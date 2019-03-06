## List & Set
JUC 集合包中的 List 和 Set 实现类包括: CopyOnWriteArrayList, CopyOnWriteArraySet 和 ConcurrentSkipListSet(基于 ConcurrentSkipListMap实现)。

![JUC_List&Set](/static/base/JUC_List&Set.jpg)
### CopyOnWriteArrayList
ArrayList 的线程安全变体，其中所有可变操作(添加、设置等)都是通过创建底层数组的新副本来实现的，
适用于集合大小通常保持较小，只读操作大大超过可变操作，并且在遍历期间需要防止线程之间的干扰。
### CopyOnWriteArraySet
HashSet 的线程安全的变体。所有操作都使用内部 CopyOnWriteArrayList 的集合，
适用于集合大小通常保持较小，只读操作大大超过可变操作，并且在遍历期间需要防止线程之间的干扰。
### ConcurrentSkipListSet
TreeSet 的线程安全的变体；基于 ConcurrentSkipListMap 的可缩放并发 NavigableSet 实现，多个线程并发安全地执行插入、删除、更新和访问操作。

## Map
JUC 集合包中 Map 的实现类包括: ConcurrentHashMap 和 ConcurrentSkipListMap。

![JUC_Map](/static/base/JUC_Map.jpg)
### ConcurrentHashMap
HashMap 的线程安全的变体，是线程安全的哈希表；它继承于 AbstractMap 类，并且实现 ConcurrentMap 接口，多个线程并发安全地执行插入、删除、更新和访问操作。
### ConcurrentSkipListMap
TreeMap 的一个线程安全的变体，是线程安全的有序的哈希表; 它继承于 AbstractMap 类，并且实现 ConcurrentNavigableMap 接口。
ConcurrentSkipListMap 是通过“跳表”来实现的，它支持并发。

## Queue
JUC 集合包中 Queue 的实现类包括: ArrayBlockingQueue, LinkedBlockingQueue, LinkedBlockingDeque, ConcurrentLinkedQueue 和 ConcurrentLinkedDeque。

![JUC_Map](/static/base/JUC_Queue.jpg)
### ArrayBlockingQueue
基于数组实现的线程安全的有界的阻塞队列，此队列按 FIFO（先进先出）原则对元素进行排序。
### LinkedBlockingQueue
基于单向链表实现的可选择边界的阻塞队列，此队列按 FIFO（先进先出）原则对元素进行排序，
与基于数组的队列相比，链表队列通常具有更高的吞吐量，但在高并发应用程序中性能的可预测性较差。
### LinkedBlockingDeque
基于双向链表实现的可选择边界的阻塞双端队列，该阻塞队列同时支持 FIFO （先进先出）和 FILO （先进后出）两种操作方式，
与基于数组的队列相比，链表队列通常具有更高的吞吐量，但在高并发应用程序中性能的可预测性较差。
### ConcurrentLinkedQueue
基于单向链表的无边界的并发队列。此队列按照 FIFO（先进先出）原则对元素进行排序，
当多个线程共享对公共集合的访问时，ConcurrentLinkedQueue 是一个合适的选择。
### ConcurrentLinkedDeque
基于双向链表实现的无边界的并发双端队列，该阻塞队列同时支持 FIFO （先进先出）和 FILO （先进后出）两种操作方式，
当多个线程共享对公共集合的访问时，ConcurrentLinkedDeque 是一个合适的选择。