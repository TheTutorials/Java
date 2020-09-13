> 订阅 [TheTutorials/Java](https://github.com/TheTutorials/Java) 学习更多 Java 相关的知识

## ArrayList 集合
在本节中我们将介绍 Java 集合框架中的 `ArrayList` 集合。不像普通数组一旦定义，长度不可以改变，`ArrayList` 长度可以根据实际需要进行扩容。并且提供了更多操作数据元素的数据结构。

![ArrayList](../images/ArrayList.png)

从 `ArrayList` 源码可以看出该类是一个泛型类
``` java
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
```

### 构造函数
* 默认无参构造函数
    ``` java
    ArrayList<String> list = new ArrayList<>();
    ```

* 指定初始容量
    ``` java
    ArrayList<String> list = new ArrayList<>(10);
    ```

* 已有 collection 初始化
    ``` java
    Collection<Integer> numbers = IntStream.range(0, 10).boxed().collect(Collectors.toSet());
    List<Integer> list = new ArrayList<>(numbers);
    ```
* 通过匿名内部类的形式构造
    ``` java
    ArrayList<Integer> numbers = new ArrayList<>(){{
        add(1);
        add(2);
        add(3);
    }};

    /* output: [1, 2, 3] */
    System.out.println(numbers);
    ```

### 添加元素到 `ArrayList`

* 尾部添加，时间复杂度: `O(1)`
    ``` java
    ArrayList<Integer> numbers = new ArrayList<>();
    numbers.add(1);
    numbers.add(2);
    numbers.add(3);

    /* output: [1, 2, 3] */
    System.out.println(numbers);
    ```

* 指定位置插入，时间复杂度: `O(n)`
    ``` java
    ArrayList<Integer> numbers = new ArrayList<>();
    numbers.add(1);
    numbers.add(0, 2);
    numbers.add(0, 3);

    /* output: [3, 2, 1] */
    System.out.println(numbers);
    ````

* 一次性插入一个集合通过 `addAll()` 方法
    ``` java
    List<String> list = List.of("Java", "Python", "C");
    ArrayList<String> languages = new ArrayList<>();
    languages.addAll(list);

    /* output: [Java, Python, C] */
    System.out.println(languages);
    ```

### 删除 `ArrayList` 中的数据元素，时间复杂度: `O(n)`
``` java
List<Integer> numbers = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10));
numbers.remove(Integer.valueOf(1)); /* 删除 1 */
numbers.remove(0); /* 删除2 */
numbers.removeIf(filter -> filter % 2 == 0); /* 删除所有的偶数 */

/* output: [3, 5, 7, 9] */
System.out.println(numbers);

numbers.removeAll(List.of(3, 9)); /* 删除3和9 */

/* output: [5, 7] */
System.out.println(numbers);
```

### 获取 `ArrayList` 数据元素

* 通过下标获取数组元素, 时间复杂度: `O(n)`
    ``` java
    ArrayList<Integer> numbers = new ArrayList<>(){{
        add(1);
        add(2);
        add(3);
    }};
    assert numbers.get(0) == 1;
    assert numbers.get(1) == 2;
    assert numbers.get(2) == 3;
    ```

* 通过 `iterator` 迭代器
    ``` java
    ArrayList<Integer> numbers = new ArrayList<>(){{
        add(1);
        add(2);
        add(3);
    }};

    /* 迭代器 */
    Iterator<Integer> iterator = numbers.iterator();

    /* output: 1 2 3 */
    while (iterator.hasNext()) {
        System.out.print(iterator.next() + " ");
    }
    System.out.println();
    ```

* 通过 `foreach` 遍历 **(推荐)**
    ``` java
    ArrayList<Integer> numbers = new ArrayList<>(){{
        add(1);
        add(2);
        add(3);
    }};

    /* output: 1 2 3  */
    for (Integer number : numbers) {
        System.out.print(number + " ");
    }
    System.out.println();
    ```

* 使用 Java8 的 `forEach()` 方法
    ``` java
    ArrayList<Integer> numbers = new ArrayList<>(){{
        add(1);
        add(2);
        add(3);
    }};

    /* output: 1 2 3  */
    numbers.forEach(number -> System.out.print(number + " "));
    ```


### 遍历过程中删除数组元素
* 使用 `Iterator` 进行迭代并且删除
    ``` java
    /* 生成1-10的数字*/
    List<Integer> list = IntStream.range(1, 11).boxed().collect(Collectors.toList());

    for (Iterator<Integer> iterator = list.iterator(); iterator.hasNext(); ) {
        if (iterator.next() % 2 == 1) {
            iterator.remove();
        }
    }

    /* output: [2, 4, 6, 8, 10] */
    System.out.println(list);
    ```

* 如果你的 `JDK` 版本是 `1.8`，可以改为下面的语句
    ``` java
    /* 生成1-10的数字*/
    List<Integer> list = IntStream.range(1, 11).boxed().collect(Collectors.toList());

    /* 删除所有的奇数 */
    list.removeIf(integer -> integer % 2 == 1);

    /* output: [2, 4, 6, 8, 10] */
    System.out.println(list);
    ```

> 注意: 不能在 `foreach` 中删除，否则会报 `ConcurrentModificationException` 异常

### `ArrayList`的`toArray()`方法

> ArrayList提供了一个将List转为数组的一个非常方便的方法，可以直接调用`toArray()`将其转换为数组

* toArray(): 可以直接将集合转换为Object数组

    ``` java
    ArrayList<Integer> arrayList = new ArrayList<>();
    arrayList.add(1);
    arrayList.add(2);
    arrayList.add(3);
    arrayList.add(4);
    Object[] objects = arrayList.toArray();
    ```


* `toArray(T[] a)`: 可以转换成指定类型的数组，当然！如果集合中的类型不一样，会抛出`ArrayStoreException`异常

    ```java
    ArrayList<Integer> arrayList = new ArrayList<>();
    arrayList.add(1);
    arrayList.add(2);
    arrayList.add(3);
    arrayList.add(4);

    Integer[] integers = new Integer[arrayList.size()];
    arrayList.toArray(integers);
    
    /* output: [1, 2, 3, 4] */
    System.out.println(Arrays.toString(integers));
    ```
* 使用 Java 8 把 `ArrayList` 转换成基本数据类型
    ``` java
    List<Integer> numbers = new ArrayList<>(){{
        add(1);
        add(2);
        add(3);
    }};

    int[] arr = numbers.stream().mapToInt(i -> i).toArray();

    /* output: [1, 2, 3] */
    System.out.println(Arrays.toString(arr));
    ```

