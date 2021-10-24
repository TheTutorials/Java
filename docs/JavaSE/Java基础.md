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