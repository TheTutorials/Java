# String 常用的方法有哪些

这个只需要看一下 `JDK` 源码就足够了

* `length()`

    Returns the length of this string.
    返回字符串长度
* `isEmpty()`

    @return {@code true} if {@link #length()} is {@code 0}, otherwise {@code false}
    判断字符串是否为空

* `charAt(int index)`
    Returns the {@code char} value at the specified index
    索引特定下表的字符

* `equals()`
     Compares this string to the specified object 判断两个对象的内容是否相等

* `startsWith(String prefix)`

    Tests if this string starts with the specified prefix. 判断字符串是否以某个字符串开始

* `endsWith(String suffix)`

    Tests if this string ends with the specified suffix.
    判断某个字符串是以某个字符串结束(后缀)

* `indexOf(int ch)` 

    Returns the index within this string of the first occurrence of
    the specified character
    返回字符串中第一次出现某个字符的下标

* ` replace(CharSequence target, CharSequence replacement)`

    Replaces each substring of this string that matches the literal target sequence with the specified literal replacement sequence

    字符串替换

* `trim()`

    Returns a string whose value is this string, with all leading and trailing space removed

    去除前后空格

*  `split(String regex)`

    Splits this string around matches of the given

    根据正则表达式分隔字符串，返回分隔后的字符数组

* `toLowerCase()` 

    Converts all of the characters in this {@code String} to lower  case using the rules of the default locale

    转换成小写字符

* `toUpperCase()` 

    Converts all of the characters in this {@code String} to upper case using the rules of the default locale.

    转换成大写
