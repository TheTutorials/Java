# `ArrayList` 和 `LinkedList` 的区别

* `ArrayList` 使用动态数组实现，而 `LinkedList` 使用双向链表组成。

## 时间复杂度分析

* `LinkedList`
    * `get(int index)` 时间复杂度为 `O(n)`，但是当我们获取第一个或者最后一个的时候这种情况时间复杂度为 `O(1)`。这种情况我们可以使用 `getFirst()` 和 `getLast()` 表示
    * `add(int index, E element)` 时间复杂度为 `O(n)`, 同理当添加的下标为 `0` 或者 `list.size() - 1` 的时候，时间复杂度也为 `O(1)`, 这种情况下我们推荐使用 `addFirst()` 和 `addLast()` 方法。
    * `remove(int index)` 时间复杂度为 `O(n)`, 同理当下标为 `0` 或者 `list.size() - 1` 的时候，时间复杂度也为 `O(1)`, 这种情况下我们可以使用 `removeFirst()` 和 `removeLast()`
    * 
* `ArrayList`

    * `get(int index)` 时间复杂度为 `O(1)`
    * `add(E e)` 时间复杂度为 `O(1)` 但是最坏的情况是需要进行扩容的时候，需要复制所有的元素到新的数组中，此时时间复杂度为 `O(n)`
    * `add(int index, E element)` 时间复杂度为 `O(n)`
    * `remove(int index)` 时间复杂度为 `O(n)`
    * 