# Java 基础

### 进制转换

十进制转二进制

### 条件控制

`if-else if-else` 分支结构

<details>
<summary>例题: 学生成绩等级判断<br/>

```
1. 90 - 100 (A等级)
2. 80 - 89 (B等级)
3. 70 - 79 (C等级)
4. 60 - 69 (D等级)
5. 0 - 59 (E等级)
6. 其他成绩非法输入
```
</summary>

``` java
System.out.print("请输入学生的成绩:");
Scanner sc = new Scanner(System.in);
int score = sc.nextInt();
if (score > 100 || score < 0) {
    System.err.println("成绩有误");
} else if (score >= 90) {
    System.out.println("A等级");
} else if (score >= 80) {
    System.out.println("B等级");
} else if (score >= 70) {
    System.out.println("C等级");
} else if (score >= 60) {
    System.out.println("D等级");
} else {
    System.out.println("E等级");
} 
```
</details>

<details>
<summary>例题: 出租车计费系统<br/>

``` 
1. 出租车计费方式：由里程钱数和等候时间钱数相加得出。
2. 里程数前3公里13元，超过3公里到15公里部分每公里2元，15公里以上部分每公里3元。
2. 等候时间每2分半1元，不足部分不要钱。
4. 输入公里数和等候秒数，输出车费
```
</summary>

``` java
System.out.print("请输入里程数(km):");
Scanner sc = new Scanner(System.in);
int km = sc.nextInt();
System.out.print("请输入等待时间(秒):");
int second = sc.nextInt();
int cost;
if (km <= 3) {
    cost = 13;
} else if (km <= 15) {
    cost = 13 + (km - 3) * 2;
} else {
    cost = 13 + (15 - 3) * 2 + (km - 15) * 3;
}
cost = cost + second / 150;
System.out.println("总需要支付:" + cost + "元");
```
</details>

`switch` 分支结构

switch 支持的数据类型
* byte
* short
* int 
* long
* String
* enum

<details>
<summary>例题: 学生成绩等级判断<br/>

```
1. 90 - 100 (A等级)
2. 80 - 89 (B等级)
3. 70 - 79 (C等级)
4. 60 - 69 (D等级)
5. 0 - 59 (E等级)
6. 其他成绩非法输入
```
</summary>

``` java
System.out.print("请输入学生的成绩:");
Scanner sc = new Scanner(System.in);
int score = sc.nextInt();

if (score >= 0 && score <= 100) {
    char level;
    switch (score / 10) {
    case 10:
    case 9:
        level = 'A';
        break;
    case 8:
        level = 'B';
        break;
    case 7:
        level = 'C';
    case 6:
        level = 'D';
        break;
    default:
        level = 'E';
        break;
    }
    System.out.println("等级" + level);
} else {
    System.err.println("成绩不合法");
}
```
</details>

<details>
<summary>例题: 实现菜单功能<br/>

```
1. 查询学生信息
2. 修改学生信息
3. 删除学生信息
4. 增加学生信息
0. 退出
```
</summary>

``` java
System.out.println("\t学生管理系统");
System.out.println("1.查询学生信息");
System.out.println("2.修改学生信息");
System.out.println("3.删除学生信息");
System.out.println("4.增加学生信息");
System.out.println("0.退出");

System.out.print("\n请输入功能编号:");
int choose = new Scanner(System.in).nextInt();

switch (choose) {
    case 1:
    System.out.println("进入了查询学生信息");
    break;
    case 2:
    System.out.println("进入修改学生信息");
    break;
    case 3:
    System.out.println("进入删除学生信息");
    break;
    case 4:
    System.out.println("进入增加学生信息");
    break;
    case 0:
    System.exit(0);
    default:
    System.err.println("编号有误");
    break;
}
```
</details>

switch 新特性
``` java
System.out.print("\n请输入功能编号:");
int choose = new Scanner(System.in).nextInt();
switch (choose) {
    case 1 -> System.out.println("1");
    case 2 -> System.out.println("2");
    case 0 -> System.exit(0);
    default -> System.err.println("other");
}
```

### 循环结构
循环是计算机科学运算领域的用语，也是一种常见的控制流程

for 循环 (当型循环)
``` java
for (statement 1; statement 2; statement 3) {
  // code block to be executed
}
```

<details>
<summary>例题: 循环打印 1 - 10
</summary>

``` java
for (int i = 1; i <= 10; ++i) {
    System.out.print(i + "\t");
}
```
</details>

<details>
<summary>例题: 循环打印 1 - 10 的所有奇数（方式一)
</summary>

``` java
for (int i = 1; i <= 10; ++i) {
    if (i % 2 == 1) {
        System.out.print(i + "\t");
    }
}
```
</details>

<details>
<summary>例题: 循环打印 1 - 10 的所有奇数（方式二)
</summary>

``` java
for (int i = 1; i <= 10; i += 2) {
    System.out.print(i + "\t");
}
```
</details>

<details>
<summary>例题: 循环打印 1 - 10 的所有奇数（方式三)
</summary>

``` java
for (int i = 1; i <= 5; ++i) {
    int item = 2 * i - 1;
    System.out.print(item + "\t");
}
```
</details>

<details>
<summary>例题: 循环计算 1 - 10 的和
</summary>

``` java
int sum = 0;
for (int i = 1; i <= 10; ++i) {
    sum += i;
}
System.out.println("1-10的和是" + sum);
```
</details>

<details>
<summary>例题: 打印1000以内的所有水仙花数字并且求和<br/>

```
在数论中，水仙花数（Narcissistic number），也被称为超完全数字不变数、自恋数、自幂数、阿姆斯壮数或阿姆斯特朗数（Armstrong number) ，用来描述一个N位非负整数，其各位数字的N次方和等于该数本身
，如 153 = 1^3 + 5^3 + 3^3
```
</summary>

``` java
int sum = 0;
for (int i = 100; i <= 999; ++i) {
    int a = i / 100; //计算百位
    int b = i / 10 % 10; //计算十位
    int c = i % 10; //计算个位
    if (a * a * a + b * b * b + c * c * c == i) {
        System.out.print(i + "\t");
        sum += i;
    }
}
System.out.println("\n水仙花数字之和是" + sum);
```
</details>

`continue` 关键词的使用
> continue 用于结束本趟循环，继续下一趟循环


<details>
<summary>例题: for + continue 打印 1-10 的奇数<br/>
</summary>

``` java
for (int i = 1; i <= 10; ++i) {
    if (i % 2 == 0) {
    continue;
    }
    System.out.print(i + "\t");
}
```
</details>

<details>
<summary>例题: 循环录入3个正整数求和，录入数据不合法，重新录入<br/>
</summary>

``` java
Scanner scanner = new Scanner(System.in);
int sum = 0;
for (int i = 1; i <= 3; ++i) {
    System.out.print("请输入第" + i + "个数:");
    int number = scanner.nextInt();
    if (number <= 0) {
        System.err.println("您输入的数字不是正整数，请重新录入");
        i--;
        continue;
    }
    sum += number;
}
System.out.println("三个正整数之和是" + sum);
```
</details>

`break` 关键词
> break 用于跳出本层循环

<details>
<summary>例题: 不断录入数字正整数求和，直到录入0停止<br/>
</summary>

``` java
Scanner scanner = new Scanner(System.in);
int sum = 0;
for (; ; ) {
    System.out.print("请输入一个数字:");
    int number = scanner.nextInt();
    if (number == 0) {
        break;
    }
    sum += number;
}
System.out.println("所有数字的和" + sum);
```
</details>

<details>
<summary>例题: 模拟两个人对话，直到某一个人说拜拜结束对话<br/>
</summary>

``` java
Scanner scanner = new Scanner(System.in);
boolean flag = true;
String firstPerson = "张三";
String secondPerson = "李四";
for (; ; ) {
    String prompt = (flag ? firstPerson : secondPerson) + ":";
    System.out.print(prompt);
    String words = scanner.nextLine();
    System.out.println(prompt + words);
    if ("拜拜".equals(words)) {
        break;
    }
    flag = !flag;
}
System.out.println("聊天结束");
```
</details>

<details>
<summary>例题: 系统随机生成一个数字，用户反复猜测，系统会提示猜大/小，直到猜测正确<br/>
</summary>

``` java
Random random = new Random();
int randomNumber = random.nextInt(100) + 1; //生成1-100之间的数字
System.out.print("系统已经为您随机生成了一个数字，请开始猜测:");
Scanner scanner = new Scanner(System.in);
int count = 0; //统计猜测的数量
for (; ; ) {
    int guessNumber = scanner.nextInt();
    count++;
    if (guessNumber < randomNumber) {
        System.out.print("猜测小了，请重新猜测:");
    } else if (guessNumber > randomNumber) {
        System.out.print("猜测大了，请重新猜测:");
    } else {
        System.out.println("恭喜您，猜对啦!");
        break;
    }
}
System.out.println("您共猜测了" + count + "次");
```
</details>

`for` 循环嵌套
> 一个for循环嵌套若干个for循环

<details>
<summary>例题: 打印5行5列的数字5<br/>

```
5	5	5	5	5
5	5	5	5	5
5	5	5	5	5
5	5	5	5	5
5	5	5	5	5
```
</summary>

``` java
for (int i = 1; i <= 5; ++i) {
    for (int j = 1; j <= 5; j++) {
        System.out.print(5 + "\t");
    }
    System.out.println();
}
```
</details>

循环嵌套的执行过程
* 外层循环循环一次，内层循环要循环多次


<details>
<summary>例题: 打印如下图形<br/>

```
*	*	*	*	*
*	*	*	*	*
*	*	*	*	*
*	*	*	*	*
*	*	*	*	*
```
</summary>

``` java
for (int i = 1; i <= 5; ++i) {
    for (int j = 1; j <= 5; ++j) {
        System.out.print('*' + "\t");
    }
    System.out.println();
}
```
</details>

<details>
<summary>例题: 打印如下图形<br/>

```
*	
*	*	
*	*	*	
*	*	*	*	
*	*	*	*	*
```
</summary>

``` java
for (int i = 1; i <= 5; ++i) {
  for (int j = 1; j <= i; ++j) {
    System.out.print('*' + "\t");
  }
  System.out.println();
}
```
</details>

<details>
<summary>例题: 打印如下图形<br/>

```
*	*	*	*	*	
*	*	*	*	
*	*	*	
*	*	
*
```
</summary>

``` java
for (int i = 5; i >= 1; --i) {
  for (int j = 1; j <= i; ++j) {
    System.out.print('*' + "\t");
  }
  System.out.println();
}
```
</details>

<details>
<summary>例题: 打印如下图形<br/>

```
*	*	*	*	*	
*	*	*	*	
*	*	*	
*	*	
*
```
</summary>

``` java
for (int i = 1; i <= 5; ++i) {
  for (int j = 1; j < i; j++) {
    System.out.print('\t');
  }
  for (int k = 1; k <= 6 - i; ++k) {
    System.out.print("*\t");
  }
  System.out.println();
}
```
</details>

<details>
<summary>例题: 打印如下图形<br/>

```
				*	
			*	*	*	
		*	*	*	*	*	
	*	*	*	*	*	*	*	
*	*	*	*	*	*	*	*	*
```
</summary>

``` java
for (int i = 1; i <= 5; ++i) {
  for (int j = 1; j <= 5 - i; j++) {
    System.out.print('\t');
  }
  for (int k = 1; k <= 2 * i - 1; ++k) {
    System.out.print("*\t");
  }
  System.out.println();
}
```
</details>

<details>
<summary>例题: 打印九九乘法表<br/>

```
1*1=1	
1*2=2	2*2=4	
1*3=3	2*3=6	3*3=9	
1*4=4	2*4=8	3*4=12	4*4=16	
1*5=5	2*5=10	3*5=15	4*5=20	5*5=25	
1*6=6	2*6=12	3*6=18	4*6=24	5*6=30	6*6=36	
1*7=7	2*7=14	3*7=21	4*7=28	5*7=35	6*7=42	7*7=49	
1*8=8	2*8=16	3*8=24	4*8=32	5*8=40	6*8=48	7*8=56	8*8=64	
1*9=9	2*9=18	3*9=27	4*9=36	5*9=45	6*9=54	7*9=63	8*9=72	9*9=81
```
</summary>

``` java
for (int i = 1; i <= 9; ++i) {
  for (int j = 1; j <= i; ++j) {
    System.out.print(j + "*" + i + "=" + j * i + "\t");
  }
  System.out.println();
}
```
</details>

<details>
<summary>例题: 打印1-100之间的所有素数<br/>

```
素数: 只能被1和它本身整出的数字，注意1不是素数
```
</summary>

``` java
System.out.println("1-100之间的所有素数如下:");
for (int i = 1; i <= 100; ++i) {
  if (i == 1) {
    continue;
  }
  boolean isPrimer = true;
  for (int j = 2; j < i; ++j) {
    if (i % j == 0) {
      isPrimer = false;
      break;
    }
  }
  if (isPrimer) {
    System.out.print(i + "\t");
  }
}
```
</details>

<details>
<summary>例题: 打印1-100之间的所有素数(优化)<br/>

```
素数: 只能被1和它本身整出的数字，注意1不是素数
```
</summary>

``` java
System.out.println("1-100之间的所有素数如下:");
for (int i = 1; i <= 100; ++i) {
  if (i == 1) {
    continue;
  }
  boolean isPrimer = true;
  for (int j = 2; j <= Math.sqrt(i); ++j) {
    if (i % j == 0) {
      isPrimer = false;
      break;
    }
  }
  if (isPrimer) {
    System.out.print(i + "\t");
  }
}
```
</details>

`while` 循环

<details>
<summary>例题: 打印1-10<br/>
</summary>

``` java
int i = 1;
while (i <= 10) {
  System.out.print(i + "\t");
  i++;
}
```
</details>

<details>
<summary>例题: 计算 1/1 + 1/2 + 1/3 + ... + 1/n<br/>
</summary>

``` java
System.out.print("请输入项数n:");
int n = new Scanner(System.in).nextInt();
double sum = 0;
int i = 1;
while (i <= n) {
  sum += 1.0 / i;
  i++;
}
System.out.println("数列前" + n + "项之和是" + sum);
```
</details>

while 循环和 for的区别
* while 适用于明确循环条件，但是不明确循环次数
* for 主要适用于明确循环次数的情况

<details>
<summary>例题: 逆序输出一个数字<br/>
</summary>

``` java
System.out.print("请输入一个数字:");
Scanner scanner = new Scanner(System.in);
int number = scanner.nextInt();
number = number < 0 ?  -number :number; //求绝对值
while (number != 0) {
  int remainder = number % 10;
  System.out.print(remainder);
  number /= 10;
}
```
</details>

<details>
<summary>例题: 逆序一个数字<br/>
</summary>

``` java
System.out.print("请输入一个数字:");
Scanner scanner = new Scanner(System.in);
int number = scanner.nextInt();
boolean isNegative = number < 0;
number = isNegative ?  -number :number; //求绝对值
int reversedNumber = 0;
int temp = number;
while (temp != 0) {
  int remainder = temp % 10;
  reversedNumber = reversedNumber * 10 + remainder;
  temp /= 10;
}
reversedNumber = isNegative ? -reversedNumber : reversedNumber;
System.out.println("数字" + number + "逆序后的结果为" + reversedNumber);
```
</details>

`do-while` 循环 

<details>
<summary>例题: 输入若干个整数求和，直到输入的数字为0结束<br/>
</summary>

``` java
Scanner scanner = new Scanner(System.in);
int sum = 0;
int number;
do {
  System.out.print("请输入一个数字:");
  number = scanner.nextInt();
  sum = sum + number;
} while (number != 0);
System.out.println("若干个数字之和是" + sum);
```
</details>

观察如下代码的执行结果
``` java
int i = 1;
while (i <= 6); {
  System.out.print(6);
  i++;
}
```

<details>
<summary>查看答案<br/>
</summary>
死循环
</details>


### 数组

一维数组的声明
``` java
数据类型[] 变量名 = new 数据类型[数组长度]
int[] array = new int[10]; //默认值为0
int array[] = new int[10]; //c语言风格
int[] array = new int[]{1, 2, 3}; //声明并初始化
int[] array = {1, 2, 3}; //简写
```

默认值
* byte，char, short，int，long，默认为0
* float, double 默认为 0.0
* boolean 默认为 false

读取数组长度
``` java
int[] nums = {1, 2, 3, 4, 5};
System.out.println("数组长度:" + nums.length);
```

下标越界
* 数组长度为`n`的数组，数组下标范围为 0 ~ n - 1，超出这个区间将抛出数组下标越界异常(ArrayIndexOutOfBoundsException)
``` java
int[] nums = {1, 2, 3, 4, 5};
System.out.println(nums[-1]); //Index -1 out of bounds for length 5
System.out.println(nums[5]); //Index 5 out of bounds for length 5
```

访问一维数组元素 (下标)
``` c
int[] nums = {1, 2, 3, 4, 5};
System.out.println("第1个元素是:" + nums[0]); //1
System.out.println("第2个元素是:" + nums[0]); //2
System.out.println("第3个元素是:" + nums[0]); //3
System.out.println("第4个元素是:" + nums[0]); //4
System.out.println("第5个元素是:" + nums[0]); //5
```

访问一维数组元素 (循环+下标)
``` c
int[] nums = {1, 2, 3, 4, 5};
for (int i = 0; i < nums.length; ++i) {
  System.out.println("第" + (i + 1) + "元素是:" + nums[i]);
}
```

访问一维数组元素 (for-each)
``` c
int[] nums = {1, 2, 3, 4, 5};
for (int num : nums) {
  System.out.print(num + "\t");
}
```

注意：数组名存放在栈空间，而真实的数据元素存储在堆空间

<details>
<summary>例题: 录入5名学生的年龄到数组中并且打印<br/>
</summary>

``` java
Scanner scanner = new Scanner(System.in);
int[] age = new int[5];
for (int i = 0; i < age.length; ++i) {
  System.out.print("请输入第" + (i + 1) + "名学生的年龄:");
  age[i] = scanner.nextInt();
}
System.out.println("5名学生的年龄如下:");
for (int i = 0; i < age.length; ++i) {
  System.out.print(age[i] + "\t");
}
```
</details>

<details>
<summary>例题: 数组任意下标位置插入元素值<br/>

```
编码实现在数组nums中任意位置插入元素值，数组中的-1表示为空
int[] nums = {1, 2, 3, 4, -1};
```
</summary>

``` java
int[] nums = {1, 2, 3, 4, -1};
Scanner scanner = new Scanner(System.in);
System.out.print("请输入要插入的下标:");
int index = scanner.nextInt();
System.out.print("请输入要插入的元素值:");
int key = scanner.nextInt();
if (index < 0 || index >= nums.length) {
  System.out.println("插入下标不合法");
} else {
  for (int i = nums.length - 2; i >= index; --i) {
    nums[i + 1] = nums[i];
  }
  nums[index] = key;
  System.out.println("插入后的数组元素如下:");
  for (int i = 0; i < nums.length; ++i) {
    System.out.print(nums[i] + "\t");
  }
}
```
</details>

<details>
<summary>例题: 数组任意下标位置插入元素值<br/>

```
编码实现在数组nums中任意位置删除元素值，删除后后续元素需要往前移动，后续元素使用0填充
int[] nums = {1, 2, 3, 4, 5}; 如删除元素2以后的结果为{1, 3, 4, 5, 0}
```
</summary>

``` java
int[] nums = {1, 2, 3, 4, 5};
Scanner scanner = new Scanner(System.in);
System.out.print("请输入要删除的数组元素下标:");
int index = scanner.nextInt();
if (index < 0 || index > nums.length - 1) {
  System.err.println("下标非法");
} else {
  System.out.println("删除的元素值是:" + nums[index]);
  for (int i = index; i < nums.length - 1; ++i) {
    nums[i] = nums[i + 1];
  }
  nums[nums.length - 1] = 0;
  System.out.println("删除后的结果如下:");
  for (int i = 0; i < nums.length; i++) {
    System.out.print(nums[i] + "\t");
  }
}
```
</details>

<details>
<summary>例题:遍历一维度数组中的所有元素，把所有奇数+1变为偶数<br/>
</summary>

``` java
int[] nums = {1, 2, 3, 4, 5};
for (int i = 0; i < nums.length; ++i) {
  if (nums[i] % 2 == 1) {
    nums[i] += 1;
  }
}
System.out.println("转换后的数组如下");
for (int num : nums) {
  System.out.print(num + "\t");
}
```
</details>

数组的优缺点
* 能够通过下标快速索引存取元素
* 所有元素的数据类型必须相同
* 内存空间必须连续，导致内存的利用率不高
* 容量不能动态增长
* 插入，删除元素又可能需要移动多个元素，时间复杂度较高


<details>
<summary>例题: 数组元素的拷贝<br/>

```
编码实现把数组nums的后n-1元素拷贝到新的数组中
int[] nums = {1, 2, 3, 4, 5}
```
</summary>

``` java
int[] nums = {1, 2, 3, 4, 5};
int[] newNums = new int[nums.length - 1];
for (int i = 1; i < nums.length; ++i) {
  newNums[i - 1] = nums[i];
}
System.out.println("拷贝后的新数组元素如下");
for (int i = 0; i < newNums.length; i++) {
  System.out.print(newNums[i] + "\t");
}
```
</details>

<details>
<summary>例题: 数组元素的拷贝(使用JDK自带的库)<br/>

```
编码实现把数组nums的后n-1元素拷贝到新的数组中
int[] nums = {1, 2, 3, 4, 5}
```
</summary>

``` java
int[] nums = {1, 2, 3, 4, 5};
int[] newNums = new int[nums.length - 1];
System.arraycopy(nums, 1, newNums, 0, nums.length - 1);
System.out.println("拷贝后的新数组元素如下");
  for (int num : newNums) {
    System.out.print(num + "\t");
  }
}
```
</details>

注意：数组的拷贝不能简单的数组名复制，如 `arrayCopy = array`，因为数组名只是存储了数组在堆区中的地址信息，而不是元素值

<details>
<summary>例题: 编码实现统计任意一个正整数每一个数字出现的次数<br/>
</summary>

``` java
Scanner scanner = new Scanner(System.in);
System.out.print("请输入一个正整数:");
int num = scanner.nextInt();
int[] countTimes = new int[10];

int temp = num;
while (temp != 0) {
  countTimes[temp % 10]++;
  temp /= 10;
}
for (int i = 0; i < countTimes.length; ++i) {
  if (countTimes[i] != 0) {
    System.out.println(i + "出现了" + countTimes[i] + "次");
  }
} 
```
</details>


<details>
<summary>例题: 统计若干个学生的成绩，并打印班级平均分<br/>
</summary>

``` java
Scanner scanner = new Scanner(System.in);
System.out.print("请输入班级人数:");
int num = scanner.nextInt();

double[] scores = new double[num];
for (int i = 0; i < scores.length; ++i) {
  System.out.print("请输入第" + (i + 1) + "个学生的成绩:");
  scores[i] = scanner.nextDouble();
}

System.out.println("班级各位学生的成绩如下:");
double sum = 0;
for (double score : scores) {
  System.out.print(score + "\t");
  sum += score;
}
System.out.println("\n班级平均分是:" + sum / scores.length);
```
</details>

`Arrays` 工具类的可以实现对数组进行多种比较常见的操作
* toString() 打印数组元素
  ``` java
  int[] nums = {1, 2, 3, 4, 5};
  System.out.println(Arrays.toString(nums)); // [1, 2, 3, 4, 5]
  ```
* fill() 填充元素
  ``` java
  int[] nums = new int[5];
  Arrays.fill(nums, 5);
  System.out.println(Arrays.toString(nums)); // [5, 5, 5, 5, 5]
  ```
* equals 数组元素的比较
  ``` java
  int[] nums1 = {1, 2, 3, 4, 5};
  int[] nums2 = {1, 2, 3, 4, 5};
  System.out.println(Arrays.equals(nums1, nums2)); // true
  ```
* sort 排序
  ``` java
  int[] nums = {1, 3, 5, 7, 9, 2, 4, 6, 8, 10}; 
  Arrays.sort(nums);
  System.out.println(Arrays.toString(nums)); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
  ```
* binarySearch() 折半查找
  ``` java
  int[] nums = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
  System.out.println(Arrays.binarySearch(nums, 1)); // 0
  System.out.println(Arrays.binarySearch(nums, 6)); // 5
  System.out.println(Arrays.binarySearch(nums, 10)); // 9
  System.out.println(Arrays.binarySearch(nums, 50)); // -11
  ```


<details>
<summary>例题: 求解数组元素的最大值(方法一:手动求解)<br/>
</summary>

``` java
int[] nums = {1, 3, 5, 7, 9, 2, 4, 6, 8};
int max = nums[0];
for (int i = 1; i < nums.length; ++i) {
  if (nums[i] > max) {
    max = nums[i];
  }
}
System.out.println("数组中的最大值是:" + max);
```
</details>

<details>
<summary>例题: 求解数组元素的最大值(方法二:排序)<br/>
</summary>

``` java
int[] nums = {1, 3, 5, 7, 9, 2, 4, 6, 8};
Arrays.sort(nums);
System.out.println("数组中的最大值是:" + nums[nums.length - 1]);
```
</details>

二维数组

声明格式
``` java
数据类型[][] 数组名 = new int[行数][列数]
```

二维数组的初始化
``` java
int[][] nums = new int[][]{
        {1, 2, 3, 4},
        {5, 6, 7, 8}
}; //每行的列数一样

int[][] nums = new int[][]{
        {1, 2, 3, 4},
        {5, 6, 7, 8},
        {9, 10},
        {11, 12, 13, 14, 15},
        {}
}; //每行的列数可以不一样

int[][] nums = new int[5][]; // 先指定行数
nums[0] = new int[1]; // 第一行的长度为1
nums[1] = new int[2]; // 第二行的长度为2
nums[2] = new int[3];
nums[3] = new int[4]; // 第三行的长度为4
nums[4] = new int[5]; // 第四行的长度为5
```

<details>
<summary>例题: 杨辉三角<br/>
</summary>

``` java
System.out.print("请输入杨辉三角的行数:");
Scanner scanner = new Scanner(System.in);
int lines = scanner.nextInt();
int[][] triangle = new int[lines][];
for (int i = 0; i < lines; ++i) {
  triangle[i] = new int[i + 1];
  for (int j = 0; j <= i; ++j) {
    if (i == j || j == 0) {
      triangle[i][j] = 1;
    } else {
      triangle[i][j] = triangle[i - 1][j] + triangle[i - 1][j - 1];
    }
  }
}

for (int i = 0; i < lines; ++i) {
  for (int j = 0; j <= i; ++j) {
    System.out.print(triangle[i][j] + "\t");
  }
  System.out.println("\n");
}
```
</details>