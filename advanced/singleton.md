Java单例模式是四中创建模式之一，本文我们讲从例子讲解单例模式的方方面面

# Java单例模式(Singleton)
* Java限制了类的实例，保证了JVM中只能存在一个某个类的一个实例

* 单实例类必须提供一个访问该实例的全局方法(其实就是`public static`)

* 单例模式使用在日志(logging)，驱动(driver)，缓存(caching)，线程池(thread pool)

* Singleton设计模式也用于其他设计模式，如Abstract Factory，Builder，Prototype，Facade等。

![java-singleton-pattern](../images/singleton.jpg)

要实现单例子模式，我们有很多不同的实现方法，但很多地方是相同的
* 私有化构造器，防止从其他类中构造实例

* 私有化该静态单例

* 定义`public static` 的 `get` 方法获取该单例，便于从其他类中获取该实例

在后面的部分中，我们将学习Singleton模式实现的不同方法以及设计实现的关注点。

1. 急切的初始化 （饿汉模式)
2. 静态代码块初始化
3. 延迟初始化 (懒汉模式)
4. 线程安全单例模式
5. Bill Pugh 单例实现
6. 使用反射来破解单例模式
7. 枚举类型的单例
8. 序列化和单例模式

### 急切的初始化
急切初始化模式，顾名思义就是当类加载时就会创建实例对象，这是实现单例模式的最简单方法，但是这样存在一个缺点就是虽然创建了该实例，但是有可能该实例不会被其他类使用，并且类的加载会变慢，因为类加载时需要创建对象

举一个例子
``` java
public class EagerInitializedSingleton {

    //私有化该实例
    private static final EagerInitializedSingleton instance = new EagerInitializedSingleton();

    //私有化构造器防止该类被其他类实例化
    private EagerInitializedSingleton() {
    }

    //提供getter方法
    public static EagerInitializedSingleton getInstance() {
        return instance;
    }
}
```

### 静态代码块初始化
这种方法和上一种方法很相似，提供一个static代码块，并提供异常处理信息
``` java
public class StaticBlockSingleton {

    private static StaticBlockSingleton instance;

    private StaticBlockSingleton() {
    }

    //在静态代码块中处理异常
    static {
        try {
            instance = new StaticBlockSingleton();
        } catch (Exception e) {
            throw new RuntimeException("Exception occured in creating singleton instance");
        }
    }

    public static StaticBlockSingleton getInstance() {
        return instance;
    }
}
```
可以看到这两种创建单实例模式都是在使用之前就创建了该实例，效率不是很高，接下来我们看看其他创建单实例的方式

### 延迟初始化 (懒汉模式)
先看例子
``` java
public class LazyInitializedSingleton {

    private static LazyInitializedSingleton instance;

    private LazyInitializedSingleton(){}

    public static LazyInitializedSingleton getInstance(){
        if(instance == null){
            instance = new LazyInitializedSingleton();
        }
        return instance;
    }
}
```
可以看到该实例的创建方式放在了public方法中了，当要使用对象时才会判断是否需要创建，这种方式对与单线程系统是安全的，但是对于多线程系统是不安全的，因为没有实现同步，

### 线程安全单例模式
先看代码
``` java
public class ThreadSafeSingleton {

    private static ThreadSafeSingleton instance;

    private ThreadSafeSingleton() {
    }

    public static synchronized ThreadSafeSingleton getInstance() {
        if (instance == null) {
            instance = new ThreadSafeSingleton();
        }
        return instance;
    }

}
```
可以看到方法上加上了`synchronized`关键词，这样多线程中同一个时刻只能有一个线程访问该方法，即锁,保证了线程安全,性能上没有没有无synchronized的高
为了避免每次额外的开销，使用双重检查锁定原理。在这种方法中，synchronized块在if条件中使用，并进行额外的检查以确保只创建一个singleton类的实例。
``` java
public class ThreadSafeSingleton {

    private static ThreadSafeSingleton instance;

    private ThreadSafeSingleton() {
    }

    public static ThreadSafeSingleton getInstanceUsingDoubleLocking() {
        if (instance == null) {
            synchronized (ThreadSafeSingleton.class) {
                if (instance == null) {
                    instance = new ThreadSafeSingleton();
                }
            }
        }
        return instance;
    }

}
```
### Bill Pug 单实例
在Java 5之前，Java内存模型有很多问题，上面实现的单例模式在很多场景下是有问题的，比如多线程环境中多个线程同时获取单例，因此Bill Pug提出了一种使用内部内创建单实例的方法
``` java
public class BillPughSingleton {

    private BillPughSingleton() {
    }

    private static class SingletonHelper {
        private static final BillPughSingleton INSTANCE = new BillPughSingleton();
    }

    public static BillPughSingleton getInstance() {
        return SingletonHelper.INSTANCE;
    }
}
```
可以看到该类中有一个静态内部内`SingletonHelper`，并在里面实现了对象的初始化，当类创建时静态内部类不会被加载，只有当`getInstance`方法被调用时，内部内才会被加载

这种方法创建单实例被广泛应用，你无须因为多线程环境而同步(synchronized)，我在我的项目中大量使用这样的方式实现单例模式，这种方法简单容易理解，并很方便实现


### 使用反射来破解单例模式
上面实现的单实例模式真的就是真的就无懈可击了么？其实不是的，我们可以通过反射机制实现创建不同的对象，即使你私有化了构造函数
``` java
public class ReflectionSingletonTest {

    public static void main(String[] args) {
        EagerInitializedSingleton instanceOne = EagerInitializedSingleton.getInstance();
        EagerInitializedSingleton instanceTwo = null;
        try {
            Constructor[] constructors = EagerInitializedSingleton.class.getDeclaredConstructors();
            for (Constructor constructor : constructors) {
                //Below code will destroy the singleton pattern
                constructor.setAccessible(true);
                instanceTwo = (EagerInitializedSingleton) constructor.newInstance();
                break;
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
        System.out.println(instanceOne.hashCode() == instanceTwo.hashCode());//output: false
    }

}
```
当你运行上面的代码，输出结果是false，说明两个对象不是同一个对象，也就是可以通过反射机制构造出不同的实例，反射机制在很多框架如Spring,Hibernate中都广泛使用


### 枚举类型的单例
为了克服这种情况，Joshua Bloch建议使用Enum来实现Singleton设计模式，因为Java确保任何枚举值只在Java程序中实例化一次。由于Java Enum值是全局可访问的，因此单例也是如此。缺点是枚举类型有些不灵活;例如，它不允许延迟初始化

``` java
public enum EnumSingleton {

    INSTANCE;

    public static void doSomething(){
        //do something
    }
}
```
