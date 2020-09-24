# `String` `StringBuilder` `StringBuffer` 之间的区别

* `StringBuffer` 的方法使用了 `synchronized` 关键词实现了同步,线程安全，也就是说不能同时有两个线程同时访问所同步的方法

* `StringBuilder` 的方法没有使用 `synchronized` 关键词同步，线程不安全，可以有两个线程同时访问

* 不考虑线程安全的情况下，`StringBuilder` 效率比 `StringBuffer` 效率高。
* `String` 是不可变对象，一旦创建无法修改，当我们对 `String` 进行频繁的 `+` 操作链接的时候其实是创建了新的对象。并且把新对象的引用赋值给 `String` 的指针，所以程序中不要出现频繁操作 `String` 的代码，如果有推荐使用 `StringBuilder`代替。