# `HashTable` 与 `HashMap` 的区别

* `HashTable` 使用了 `synchronized` 进行线程同步，而 `HashMap` 没有实现同步,这使得在非线程安全的的应用程序情况下，`HashMap` 效率比 `synchronized` 的 `HashTable` 更高。

* `HashTable` 既不允许 `key` 为 `null`， 也不允许 `value` 为 `null`,而 `HashMap` `key` 和 `value` 都可以为空

    ``` java
    /* 报空指针异常 */
    hashtable.put("name", null); 
    hashtable.put(null, null);

    /* no exception occur */
    hashMap.put(null, null);
    hashMap.put(null, null);
    ```
* HashMap的子类之一是LinkedHashMap，因此，如果您想要可预测的迭代顺序（默认情况下为插入顺序），则可以轻松地将HashMap换成LinkedHashMap。如果您使用的是Hashtable，这将不那么容易。

> 如果不需要线程同步安全问题，则考虑使用 `HashMap`， 如果应用程序需要考虑 `ConcurrentHashMap`


reference: https://stackoverflow.com/questions/40471/what-are-the-differences-between-a-hashmap-and-a-hashtable-in-java