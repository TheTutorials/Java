# 如何反转一个字符串
我们可以使用下面的方式实现字符串的反转

* 使用 `StringBuilder` 的 `reverse()` 方法
* 使用 `StringBuffer` 的 `reverse()` 方法
* 把 `String` 转换成字符数组，然后头尾逐个交换。

请参考如下代码
> https://github.com/TheAlgorithms/Java/blob/master/strings/ReverseString.java
``` java
/**
 * Reverse String using different version
 */
public class ReverseString {

    public static void main(String[] args) {
        assert reverse("abc123").equals("321cba");
        assert reverse2("abc123").equals("321cba");
    }

    /**
     * easiest way to reverses the string str and returns it
     *
     * @param str string to be reversed
     * @return reversed string
     */
    public static String reverse(String str) {
        return new StringBuilder(str).reverse().toString();
    }

    /**
     * second way to reverses the string str and returns it
     *
     * @param str string to be reversed
     * @return reversed string
     */
    public static String reverse2(String str) {

        if (str == null || str.isEmpty()) {
            return str;
        }
        
        char[] value = str.toCharArray();
        for (int i = 0, j = str.length() - 1; i < j; i++, j--) {
            char temp = value[i];
            value[i] = value[j];
            value[j] = temp;
        }
        return new String(value);
    }

}
```

# reference
https://stackoverflow.com/questions/7569335/reverse-a-string-in-java