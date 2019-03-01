![Collection结构图](/static/base/Collection.jpg)

# Collection

## List

### LinkedList
是双向链表实现的双端队列；它不是线程安全的，只适用于单线程。
### ArrayList
是数组实现的队列，它是一个动态数组；它也不是线程安全的，只适用于单线程。
### Vector
是数组实现的矢量队列，它也一个动态数组；不过和ArrayList不同的是，Vector是线程安全的，它支持并发。
### Stack
是Vector实现的栈；和Vector一样，它也是线程安全的。

## Set
### HashSet
是一个没有重复元素的集合，它通过HashMap实现的；HashSet不是线程安全的，只适用于单线程。
### TreeSet
也是一个没有重复元素的集合，不过和HashSet不同的是，TreeSet中的元素是有序的；它是通过TreeMap实现的；TreeSet也不是线程安全的，只适用于单线程。

# Map

## HashMap
是存储“键-值对”的哈希表；它不是线程安全的，只适用于单线程。
## WeakHashMap
是也是哈希表；和HashMap不同的是，HashMap的“键”是强引用类型，而WeakHashMap的“键”是弱引用类型，也就是说当WeakHashMap 中的某个键不再正常使用时，
会被从WeakHashMap中被自动移除。WeakHashMap也不是线程安全的，只适用于单线程。
## HashTable
也是哈希表；和HashMap不同的是，Hashtable是线程安全的，支持并发。
## TreeMap
也是哈希表，不过TreeMap中的“键-值对”是有序的，它是通过R-B Tree(红黑树)实现的；TreeMap不是线程安全的，只适用于单线程。
