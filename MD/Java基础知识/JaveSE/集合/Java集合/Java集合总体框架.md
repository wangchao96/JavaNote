Java集合主要可以划分为4个部分：List列表、Set集合、Map映射、工具类(Iterator迭代器、Enumeration枚举类、Arrays和Collections)。

![Java集合](/static/base/Collection.jpg)

# List

## LinkedList
双向链表实现的双端队列；它不是线程安全的，只适用于单线程。
## ArrayList
数组实现的队列，它是一个动态数组；它也不是线程安全的，只适用于单线程。
## Vector
数组实现的矢量队列，它也一个动态数组；不过和ArrayList不同的是，Vector是线程安全的，它支持并发。
## Stack
Vector实现的栈；和Vector一样，它也是线程安全的。

# Set
## HashSet
没有重复元素的集合，它通过HashMap实现的；HashSet不是线程安全的，只适用于单线程，不保证集合的迭代顺序，特别是它不能保证顺序随时间保持不变。
## TreeSet
没有重复元素的集合，不过和HashSet不同的是，TreeSet中的元素是有序的；它是通过TreeMap实现的；TreeSet也不是线程安全的，只适用于单线程。

# Map

## HashMap
存储“键-值对”的哈希表；它不是线程安全的，只适用于单线程，不保证映射的顺序，特别是它不能保证顺序随时间保持不变。
## WeakHashMap
哈希表；和HashMap不同的是，HashMap的“键”是强引用类型，而WeakHashMap的“键”是弱引用类型，也就是说当WeakHashMap 中的某个键不再正常使用时，
会被从WeakHashMap中被自动移除。WeakHashMap也不是线程安全的，只适用于单线程。
## HashTable
哈希表；和HashMap不同的是，HashTable是线程安全的，支持并发。
## TreeMap
基于红黑树实现的哈希表，TreeMap中的“键-值对”是有序的，它是通过R-B Tree(红黑树)实现的；TreeMap不是线程安全的，只适用于单线程。

# 工具类

## Iterator迭代器
遍历集合的工具，即我们通常通过Iterator迭代器来遍历集合。我们说Collection依赖于Iterator，是因为Collection的实现类都要实现iterator()函数，返回一个Iterator对象。
ListIterator是专门为遍历List而存在的。
## Enumeration枚举类
JDK 1.0引入的抽象类。作用和Iterator一样，也是遍历集合；但是Enumeration的功能要比Iterator少。在上面的框图中，Enumeration只能在HashTable, Vector, Stack中使用。
## Arrays
该类包含用于操作数组的各种方法(例如排序和搜索)。该类还包含一个静态工厂，允许将数组视为列表。
## Collections
该类只由对集合进行操作或返回集合的静态方法组成。它包含对集合进行操作的多态算法、返回由指定集合支持的新集合的“包装器”，以及其他一些零碎的东西。