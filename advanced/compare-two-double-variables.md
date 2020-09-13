> 订阅 [TheTutorials/Java](https://github.com/TheTutorials/Java) 学习更多 Java 相关的知识

## Java 如何比较两个小数

在 Java 程序设计语言中，小数的比较不能单纯的使用关系运算符 `>`, `<`, `==` 等进行比较，因为比较的时候会存在精度的丢失。
举个例子，下面的代码输出不是 `true` 而是 `false`
``` java
double a = 1.000001;
double b = 0.000001;
double c = a - b;

/* output: false */
System.out.println(a - b == 1.0);
```

## 如何比较两个小数字是否相等 
* 方法一: 使用误差值
    ``` java
    double a = 1.000001;
    double b = 0.000001;
    double c = a - b;

    /* output: true */
    System.out.println(Math.abs(c - 1.0) <= 0.000001);
    ```
* 使用 `BigDecimal` 类

    我们可以使用 `BigDecimal` 进行高精度算术运算
    ``` java
    BigDecimal a = new BigDecimal("1.000001");
    BigDecimal b = new BigDecimal("0.000001");
    BigDecimal c = a.subtract(b); /* c = a - b */

    /* output: true */
    System.out.println(c.equals(new BigDecimal("1.000000")));
    ```
* 使用 `Double.compare` 方法
    ``` java
    double a = 0.0000001;
    double b = 0.0000001;

    /* output: true */
    System.out.println(Double.compare(a, b) == 0);
    ```