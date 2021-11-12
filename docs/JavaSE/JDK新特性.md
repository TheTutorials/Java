# JDK 新特性

## Stream 流

<details>
<summary>例题:  Stream 遍历 list 集合(lamda表达式)<br/>
</summary>

``` java
List<String> list = List.of("Java", "Python", "C", "HTML", "Python");
list.forEach(item -> System.out.println(item)); // Java Python C HTML Python
```
</details>

<details>
<summary>例题:  Stream 遍历 list 集合(函数引用形式)<br/>
</summary>

``` java
List<String> list = List.of("Java", "Python", "C", "HTML", "Python");
list.forEach(item -> System.out.println(item)); // Java Python C HTML Python
```
</details>