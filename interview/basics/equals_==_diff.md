# `equals` 方法和 `==` 的区别

* `==` 两端如果是基本数据类型，则比较的是 `==` 两端的数值是否相等,如果是引用数据类型比较的是引用(内存地址)是否相同，即判断是否指向同一个对象。

    ``` java
    System.out.println(1 == 1); /* true */
    System.out.println("abc123" == "abc123"); /* true */

    String str1 = "ABC";
    String str2 = "ABC";
    String str3 = new String("ABC");
    System.out.println(str1 == str2); /* true */
    System.out.println(str2 == str3); /* false */
    ```
    注意: `str1` 和 `str2` 都指向常量池中的字符串常量，则地址相等，而 `str3` 重新开辟了空间，不指向常量池中的字符串。所以地址不一样。

* 如果一个类或者该类的父类没有覆盖 `Object` 的 `equals` 方法，则调用 `equals` 方法比较的是两个对象是否是同个对象。源码如下
    ``` java
    public boolean equals(Object obj) {
        return (this == obj);
    }
    ```

* 如果想要 `equals` 方法进行值的比较而不是引用（地址）比较的话，则需要覆盖 `equals` 方法。我们自定义的普通类默认都是继承 `Object` 类，`eqauls` 方法并没有重写，请看如下代码。

    ``` java
    class User {
        private String name;

        public User(String name, int age) {
            this.name = name;
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        User user1 = new User("Tom", 23);
        User user2 = new User("Tom", 23);
        System.out.println(user1.equals(user2)); /* false */
    }
    ```
    上面代码之所以打印 `false` 是因为 `User` 类没有重写 `Object` 的 `equals` 方法。如果我们重写，则会按照 `equals` 方法的逻辑比较。请再看如下代码

    ``` java
    String str1 = new String("TheTutorials");
    String str2 = new String("TheTutorials");
    System.out.println(str1.equals(str2)); /* true */
    ```
    之所以输出 `true` 是因为 `String` 类重写了 `equals` 方法

    不同版本的 `JDK` 重写的方法有可能有差别
    ``` java
    public boolean equals(Object anObject) {
        if (this == anObject) {
            return true;
        }
        if (anObject instanceof String) {
            String aString = (String)anObject;
            if (coder() == aString.coder()) {
                return isLatin1() ? StringLatin1.equals(value, aString.value)
                                  : StringUTF16.equals(value, aString.value);
            }
        }
        return false;
    }
    ```
* 如果您重写 `equals`，请始终记住重写 `hashCode()` 方法，如果两个对象的`equals()` 方法表明它们相等，则从`hashCode()`方法返回的结果必须相同。相反，不一定是正确的。