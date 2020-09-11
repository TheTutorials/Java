## 数组
> 数组是编程语言中最常见的一种数据结构，可以存储多个数据，每一个数组元素存放一个数据，可以通过数组的下标(索引)来访问数组元素

---
## 理解数组
> 在Java中，一个数组要求具有相同的数据类型，一旦数组初始化完成，那么数组在内存中所占用的空间将被固定下来，所以说，数组的长度是不可改变的，就算是把某个数组元素清空，也同样会被保留空间，依然属于这个数组。
Java的数组既可以存储基本数据类型，也可以存储引用数据类型，唯一的条件就是要求具有相同的数据类型。

---
## 定义数组
> Java中定义数组有两种方式，如下，推荐使用第一行那种方式，有着更直观的语意，并且还具有更好地可读性

```java
int[] arr1;
int arr2[];
```
> 数组是一种引用类型的变量，因此使用它定义一个变量时，仅仅表示定义了一个引用变量（等于定义了一个指针），这个引用变量还未指向任何有效的内存，因此定义数组时不能指定数组的长度。而且由于定义数组只是定义了一个引用类型变量，并未指向任何有效的内存空间，所以还没有空间来存储数组元素，因此，这个数组也不能够被使用，只有对数组完成初始化后才能够使用。

---
### 数组的初始化
> Java中数组必须先初始化后才能够被使用，初始化就是为数组分配指定的内存空间，并给数组赋初始值。

有两种初始化的方式：

- 静态初始化：初始化时直接指定每个元素的初始值，由系统决定数组长度。
- 动态初始化：初始化时直接指定数组长度，由系统为数组分配初始值。

#### 静态初始化
假如我现在定一个int类型数组：
初始化数组时候直接在花括号中写好对应的值，系统会自动确定数组的长度，此时这个arr数组内部就有了1到10这些int类型的值。

```java
int[] arr = new int[]{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
```

当然，还有一种写法也可行：

```java
int[] arr = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
```

#### 动态初始化
假如我现在定一个int类型长度为10的数组：
动态初始化时候指定数组的长度，系统会自动为数组内部元素指定初始值

```java
 int[] arr = new int[10];
```

数组的类型可以是整数类型、浮点类型、字符类型、布尔类型和引用类型。

---

## 数组的使用
数组的使用包括取出数组元素和赋值数组。访问数组元素是通过在数组后紧跟 “[ ]” ，就可以根据括号中的索引值查找元素或者赋值。在Java中数组下标索引是从0开始的，所以，最后一个元素下标索引是数组长度减1。下面来看看基本使用方法（取出和赋值）。

```java
public class Main {

    public static void main(String[] args) {

        int[] arr = new int[]{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

        int number1 = arr[0];
        int number2 = arr[1];

        System.out.println(number1);//将输出1
        System.out.println(number2);//将输出2

        arr[0] = 100;

        System.out.println(arr[0]);//将输出100

    }
}

```

以上都是操作数组的正常方式，从1 - 10共有10个元素，但是如果我们取第11个会发生什么呢？

```java
public class Main {

    public static void main(String[] args) {

        int[] arr = new int[]{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
        int number1 = arr[11];

    }
}

```
抛出异常了，数组越界！
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191223234043151.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9teWh1Yi5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

还有一种情况，如果下标索引是负数呢？
同样，也是抛出异常，越界！
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019122323413287.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9teWh1Yi5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

所以说，访问数组下标不能够超出（数组长度-1），且下标索引必须大于等于0。

### 数组的遍历

```java
public class Main {

    public static void main(String[] args) {

        int[] arr = new int[]{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

        //可以通过数组.length拿到数组长度
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }

    }
}
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191223234658265.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9teWh1Yi5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

### 数组的赋值
基本创建数组已经会了，假如我只给数组初始化长度，不给赋值会输出什么呢？下面来看看效果：
用int类型来试试

```java
public class Main {

    public static void main(String[] args) {

        int[] arr = new int[10];

        //可以通过数组.length拿到数组长度
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }

    }
}
```
结果默认值全是0
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191223234749675.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9teWh1Yi5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

如果是String类型呢？

```java
public class Main {

    public static void main(String[] args) {

        String[] arr = new String[10];

        //可以通过数组.length拿到数组长度
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }

    }
}
```

结果全是null（为空）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191223234837868.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9teWh1Yi5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

可见，只要符合创建数组，不赋值的情况下，数组会自动分配默认值。

---

## 数组的深入理解
> 数组是一种引用数据类型，数组引用变量只是一个引用，数组元素和数组变量在内存中是分开来存放的。

### 内存中的数组
> 数组引用变量只是一个引用，引用变量可以指向任何有效的内存，只有当前引用指向有效的内存中，才能通过该数组变量来访问数组元素。
> 实际的数组对象被存在堆内存中，如果引用该数组对象的数组引用变量是一个局部变量，那么它被存放在栈内存中。
> 如果堆内存中不再有任何变量引用自己，则这个数组将成为垃圾，该数组所占的内存将会被垃圾回收机制回收。

### 多维数组
多维数组，顾名思义，就是有多个维度的数组（只是先这么理解，其实是不存在的），比如初始化一个数组，像以上初始化，那么都是一维数组，下面来定义一个二维数组：
这代表了5行5列的数组：

```java
public class Main {

    public static void main(String[] args) {

        int[][] arr = new int[5][5];

    }
}
```

我们来进行初始化：

```java
public class Main {

    public static void main(String[] args) {

        int[][] arr = new int[][]{
                {1, 2, 3, 4, 5},
                {1, 2, 3, 4, 5},
                {1, 2, 3, 4, 5},
                {1, 2, 3, 4, 5},
                {1, 2, 3, 4, 5}
        };

    }
}
```
同样，引用下标也是如此，比如说引用第二行，第三列的的一个元素:

```java
public class Main {

    public static void main(String[] args) {

        int[][] arr = new int[][]{
                {1, 2, 3, 4, 5},
                {1, 2, 3, 4, 5},
                {1, 2, 3, 4, 5},
                {1, 2, 3, 4, 5},
                {1, 2, 3, 4, 5}
        };

        int number = arr[1][2];
        System.out.println(number);

    }
}

```

同理，我也可以定义一个三维数组：


```java
public class Main {

    public static void main(String[] args) {

        int[][][] arr = new int[][][]{
                {
                        {1, 2, 3, 4, 5, 6},
                        {1, 2, 3, 4, 5, 6},
                        {1, 2, 3, 4, 5, 6}
                }, {
                        {1, 2, 3, 4, 5, 6},
                        {1, 2, 3, 4, 5, 6},
                        {1, 2, 3, 4, 5, 6}
                }, {
                        {1, 2, 3, 4, 5, 6},
                        {1, 2, 3, 4, 5, 6},
                        {1, 2, 3, 4, 5, 6}
                }, {
                        {1, 2, 3, 4, 5, 6},
                        {1, 2, 3, 4, 5, 6},
                        {1, 2, 3, 4, 5, 6}
                }
        };

        int number = arr[1][2][3];
        System.out.println(number);

    }
}
```

### 增强工具类 Arrays
Arrays包含了很多静态方法，见注释

```java
import java.util.Arrays;

public class Main {

    public static void main(String[] args) {

        int[] arr = new int[]{1, 2, 3, 4, 5, 6, 7, 8, 9};

        //使用二分查找查询key元素在arr数组中出现的索引，如果arr数组中不包括key元素的值，则返回负数。
        //要求：该数组元素已经升序排列。
        int i = Arrays.binarySearch(arr, 3);
        System.out.println(i);//输出2

        //与第一种类似，但是只搜索2 - 6 索引的值。同理，要求已经升序排列。
        int i2 = Arrays.binarySearch(arr, 2, 6, 3);
        System.out.println(i2);//输出2

        //根据arr数组复制出来一个新数组，15代表的是复制出来新数组的长度，arr长度为9，但是这里大于就，则会往数组中添加默认值，凑够15为止。
        int[] ints = Arrays.copyOf(arr, 15);

        //也是复制数组，但是只会复制从索引2到索引5的元素
        int[] ints2 = Arrays.copyOfRange(arr, 2, 5);

        //将所有数组元素都赋值为0，无返回值
        Arrays.fill(arr, 0);

        //将下标索引2-5元素赋值为0
        Arrays.fill(arr, 2, 5, 0);

        //将数组排序,无返回值
        Arrays.sort(arr);

        //只会排序下标2到5的元素，无返回值
        Arrays.sort(arr, 2, 5);

        //将数组转化为String字符串
        String s = Arrays.toString(arr);
        
    }
}
```
