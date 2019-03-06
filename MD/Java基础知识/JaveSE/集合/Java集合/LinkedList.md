## 简介
* LinkedList是一个双向链表实现的双端队列；可以当作栈、队列或双端队列使用。
* LinkedList 实现 List 接口，能对它进行队列操作。
* LinkedList 实现 Deque 接口，即能将LinkedList当作双端队列使用。
* LinkedList 实现了 Cloneable 接口，即覆盖了函数 clone()，能被克隆。
* LinkedList 实现 java.io.Serializable 接口，这意味着 LinkedList 支持序列化，能通过序列化去传输。
* LinkedList 是非同步的。

## 数据结构
![LinkedList](/static/base/LinkedList.jpg)

LinkedList 包含两个重要的成员：header 和 size。
* header 是双向链表的表头，它是双向链表节点所对应的类 Entry 的实例。
Entry 中包含成员变量： previous, next, element。
其中，previous 是该节点的上一个节点，next 是该节点的下一个节点，element 是该节点所包含的值。 
* size 是双向链表中节点的个数。

## 源码解析

...

总结：
* LinkedList 实际上是通过双向链表去实现的。
它包含一个非常重要的内部类：Entry。Entry 是双向链表节点所对应的数据结构，它包括的属性有：当前节点所包含的值，上一个节点，下一个节点。
*LinkedList实际上是通过双向链表去实现的。既然是双向链表，那么它的顺序访问会非常高效，而随机访问效率比较低。
既然LinkedList是通过双向链表的，但是它也实现了List接口。LinkedList是如何实现随机访问，如何将“双向链表和索引值联系起来的”？
实际原理非常简单，它就是通过一个计数索引值来实现的。例如，当我们调用get(int location)时，首先会比较“location”和“双向链表长度的1/2”；
若前者大，则从链表头开始往后查找，直到location位置；否则，从链表末尾开始先前查找，直到location位置。
这就是“双线链表和索引值联系起来”的方法。
* LinkedList 实现java.io.Serializable。当写入到输出流时，先写入“容量”，再依次写入“每一个节点保护的值”；当读出输入流时，先读取“容量”，再依次读取“每一个元素”。
* 由于LinkedList实现了Deque，而 Deque 接口定义了在双端队列两端访问元素的方法。提供插入、移除和检查元素的方法。
每种方法都存在两种形式：一种形式在操作失败时抛出异常，另一种形式返回一个特殊值（null 或 false，具体取决于操作）。


