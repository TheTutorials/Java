# String 可以被继承么

从 `JDK` 源码我们可以发现 `String` 类被 `final` 关键词所修饰，所以没有办法去继承 `String` 类

``` java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence,
               Constable, ConstantDesc {
    ...
    ...
```