## Final 关键词
Java 中的关键词 `final` 可以理解为最终,不可变的意思。下面介绍 `final` 的使用场景。

* 修饰普通变量
    > 当一个变量使用 `final` 声明时。它的值不能被二次修改
    ``` java
    final double PI = 3.1415927;
    /* cannot assign a value to final variable PI */
    PI = 3.1415928;
    ```

    > 如果 `final` 声明变量时候没有初始化，则无法使用该变量(所以必须先初始化)
    ``` java
    final double PI;
    /* variable PI might not have been initialized */
    double area = PI * 5 * 5;
    ```
* 修饰对象
    > 当一个引用类型的变量使用 `final` 修饰时。不能重新指向另外的对象，但是可以修改对象的内容
    ``` java
    final List<Integer> list = new ArrayList<>();
    /* 可以修改对象的内容 */
    list.add(1);
    list.add(2);
    list.add(3);

    /* output: [1, 2, 3] */
    System.out.println(list);

    /* cannot assign a value to final variable list */
    list = new ArrayList<>();
    ```

* 修饰类
    > 当 `final` 修饰类时，该类无法被当作父类继承,所以如果不想让类被继承只需要使用  `final` 修饰即可。比如 `Integer` 和 `String` 类
    ``` java
    final class A {
        /* do something */
    }

    /* cannot inherit from final A */
    class B extends A {
        /* do something */
    }
    ```

* 修饰方法
    > 当 `final` 修饰父类方法时，子类无法覆盖(重写)父类方法
    ``` java
    class A {
        public final void method() {
            /* do something */
        }
    }

    class B extends A {
        /* B cannot override method() in A overridden method is final*/
        public void method() {
            /* do something */
        }
    }
    ```

* 修饰方法参数
    > 当 `final` 修饰方法参数时，不能在方法体内修改参数的值
    ``` java
    public void methodWithFinalArguments(final int x) {
        /* final parameter x may not be assigned */
        x = 1;
    }
    ```
    
---
    
## 使用final关键字好处
> 1.final关键字提高了性能。JVM和Java应用都会缓存final变量<br/>
> 2.final变量可以安全的在多线程环境下进行共享，而不需要额外的同步开销<br/>
> 3.使用final关键字，JVM会对方法、变量以及类进行优化<br/>

---

## reference

> 1.https://www.baeldung.com/java-final<br/>2.https://stackoverflow.com/questions/15655012/how-does-the-final-keyword-in-java-work-i-can-still-modify-an-object<br/>3.https://www.geeksforgeeks.org/final-keyword-java/
