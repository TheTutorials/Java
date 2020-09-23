# Math.round(-1.5) 结果为多少

请看如下代码
``` java
System.out.println(Math.round(-1.4)); /* -1 */
System.out.println(Math.round(1.4)); /* 1 */

System.out.println(Math.round(-1.5)); /* -1 */
System.out.println(Math.round(1.5)); /* 2 */

System.out.println(Math.round(-1.6)); /* -2 */
System.out.println(Math.round(1.6)); /* 2 */
```

该函数的声明如下
``` java
* @return  the value of the argument rounded to the nearest
*          {@code long} value.
* @see     java.lang.Long#MAX_VALUE
* @see     java.lang.Long#MIN_VALUE
*/
public static long round(double a) {
```
> 四舍五入到最接近的值