> 订阅 [TheTutorials/Java](https://github.com/TheTutorials/Java) 学习更多 Java 相关的知识

## 深入理解 `String` 类
Java 中的 `String` 表示一个字符序列(字符串)。这是一个不可变的对象，一旦创建不能修改。

可以通过查看源码观察 `String` 的 类声明
``` java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence,
               Constable, ConstantDesc {
```

> 之前的 `JDK` 版本中 `String` 底层使用的是（`char`）数组保存字符，而最新的 `JDK` 版本中使用的是 `byte` 数组保存字符，因为 `char` 占用2字节， 而 `byte` 占用1个字节。这样子可以节省空间的消耗。

### `String` 构造函数 (常见的构造方法:不需要去记忆，打开源代码就可以查看到)
``` java
String()
String(String original)
String(char value[])
String(char value[], int offset, int count)
String(int[] codePoints, int offset, int count)
String(byte bytes[], int offset, int length, String charsetName)
String(byte bytes[], int offset, int length, Charset charset)
```

### 创建 `String` 对象
``` java
String name = "TheTutorials"; /* 字符串常量(推荐) */
String name = new String("TheTutorial"); /* 使用 new 关键词(不推荐) */

String name = new String(new byte[]{84, 104, 101, 84, 117, 116, 111, 114, 105, 97, 108}); /* 使用 byte 数组*/
/* output: TheTutorial */
System.out.println(name);

/* 指定字符集编码 */
String name = new String(new byte[]{84, 104, 101, 84, 117, 116, 111, 114, 105, 97, 108}, Charset.defaultCharset());

String name = new String(new byte[]{84, 104, 101, 84, 117, 116, 111, 114, 105, 97, 108}, StandardCharsets.UTF_8);

String name = new String(new StringBuilder("TheTutorial")); /* 从 StringBuilder 构造 */
String name = new String(new StringBuffer("TheTutorial")); /* 从 StringBuffer 构造 */
```

### `String` 常用方法
``` java
assert name.length() == 12;
assert name.charAt(0) == 'T' && name.charAt(3) == 'T';
assert !name.isEmpty();
assert name.equals("TheTutorials");
assert name.equalsIgnoreCase("thetutorials");
assert name.compareTo("TheTutorials") == 0;
assert name.startsWith("T") && name.startsWith("The");
assert name.endsWith("s") && name.endsWith("Tutorials");
assert name.indexOf('T') == 0;
assert name.indexOf("The") == 0;
assert name.lastIndexOf('T') == 3;
assert name.replace("Tutorials", "-Tutorials").equals("The-Tutorials");
assert name.equals(" TheTutorials ".trim());
assert name.toUpperCase().equals("THETUTORIALS");
assert name.toLowerCase().equals("thetutorials");
```
更多方法请查看源码，没必要都记住(我也记不住)，记不住的时候看看源码就知道了 :)


### 关于 `String` 的常见问题
* `String` 转换成整数
    ```java
    int foo = Integer.parseInt("1234");
    assert foo == 1234;
    ```
    如果无法转换则会抛出 `NumberFormatException` 异常
    ``` java
    try {
        int foo = Integer.parseInt("1234a");
    } catch (NumberFormatException e) {
        /* do something */
    }
    ```
* `ArrayList` 转换成 `String[]`
    ``` java
    List<String> os = new ArrayList<>() {{
        add("Unix");
        add("Android");
        add("Windows");
        add("Linux");
        add("Mac OS X");
    }};
    String[] os1 = os.toArray(String[]::new);

    /*
        * Output:
        * Unix
        * Android
        * Windows
        * Linux
        * Mac OS X
        */
    for (String item : os1) {
        System.out.println(item);
    }
    ```
* 生成一个随机字符串(包含字母和数字)
    ``` java
    String randomString = UUID.randomUUID().toString().replace("-", "");
    
    /* output: 0a03a92faff840a69daca3f0d5da7216 */
    System.out.println(randomString);
    ```

### references
1. https://stackoverflow.com/questions/5585779/how-do-i-convert-a-string-to-an-int-in-java/5585800
2. https://stackoverflow.com/questions/4042434/converting-arrayliststring-to-string-in-java/4042464
3. https://stackoverflow.com/questions/41107/how-to-generate-a-random-alpha-numeric-string
4. https://www.geeksforgeeks.org/string-class-in-java/