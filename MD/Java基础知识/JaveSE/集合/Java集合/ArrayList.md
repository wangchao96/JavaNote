## 简介
* 数组实现的队列，它是一个动态数组；它也不是线程安全的，只适用于单线程。
* 继承于AbstractList，实现了List, RandomAccess, Cloneable, java.io.Serializable 接口。
* ArrayList 继承了 AbstractList，实现了 List。它是一个数组队列，提供了相关的添加、删除、修改、遍历等功能。
* ArrayList 实现了 RandomAccess 接口，即提供了随机访问功能。RandomAccess 是 java 中用来被 List 实现，为 List 提供快速访问功能的。
在 ArrayList 中，我们即可以通过元素的序号快速获取元素对象；这就是快速随机访问。
* 此类的 iterator 和 listIterator 方法返回的迭代器是快速失败的：在创建迭代器之后，除非通过迭代器自身的 remove 或 add 方法从结构上对列表进行修改，
否则在任何时间以任何方式对列表进行修改，迭代器都会抛出 ConcurrentModificationException。因此，面对并发的修改，迭代器很快就会完全失败。
## 数据结构
![ArrayList](/static/base/ArrayList.jpg)

ArrayList 包含了两个重要的对象：elementData 和 size。

* elementData 是 Object[] 类型的数组，它保存了添加到ArrayList中的元素。
实际上，elementData是个动态数组，我们能通过构造函数 ArrayList(int initialCapacity)来执行它的初始容量为initialCapacity；
如果通过不含参数的构造函数ArrayList()来创建ArrayList，则elementData的容量默认是10。
elementData数组的大小会根据ArrayList容量的增长而动态的增长，具体的增长方式，请参考源码分析中的ensureCapacity()函数。

* size 是动态数组的实际大小。
## 源码解析

...

总结：
* ArrayList 实际上是通过一个数组去保存数据的。当我们构造 ArrayList 时；若使用默认构造函数，则 ArrayList 的默认容量大小是10。
* ArrayList 容量不足以容纳全部元素时，ArrayList 会重新设置容量：newCapacity = oldCapacity + (oldCapacity >> 1)。
* ArrayList 的克隆函数，即是将全部元素克隆到一个数组中。
* ArrayList 实现 java.io.Serializable 的方式。当写入到输出流时，先写入“容量”，再依次写入“每一个元素”；当读出输入流时，先读取“容量”，再依次读取“每一个元素”。

