# Java 基础

### 进制转换

十进制转二进制

### 条件控制

`if-else if-else` 分支结构

<details>
<summary>例题: 学生等级判断<br/>

```
90 - 100 分优秀，80 - 89 分良好，60 - 79 中等，60分以下偏差，其余情况成绩有误
```
</summary>

``` java
System.out.print("请输入学生的成绩:");
Scanner sc = new Scanner(System.in);
int score = sc.nextInt();
if (score > 100 || score < 0) {
    System.err.println("成绩有误");
} else if (score >= 90) {
    System.out.println("优秀");
} else if (score >= 80) {
    System.out.println("良好");
} else if (score >= 60) {
    System.out.println("中等");
} else {
    System.out.println("偏差");
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
