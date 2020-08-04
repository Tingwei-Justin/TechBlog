### Set

A collection that can not contain duplicate elements

- **HashSet:** which stores its elements in a hash table, but no guarantees the order
- **TreeSet:** which stores its elements in a red-black tree, orders its elements based on their values
  - custom define a comparator. 增删查改 都是 O(log n)
- **LinkedHashSet:** it is a hashset and also it is a linkedlist, it maintains the order when each of the elements is inserted into the hashset.
  - 当不需要顺序遍历的时候，不需要用linkedhashset, 因为很多overhead



### Map

A collection that stores <key, value> pairs, and no duplicated keys are allowed



How is HashMap represented internally?

- array of entries

- each entry is actually a singly linked list (handle collision)

  

What are the steps for hashmap to get the key

- Step 1: key -> hashcode

- Step 2: hashcode -> index

- Step 3: from the corresponding singley linked list, iterate all of nodes to find if the same key exists



How does hashmap compute hashCode and compare keys?

- use key.hashCode() to determine the entry index for the key
- use key.equals() to determine whether two keys are the same key



- HashMap
  - allow null for 1 key and allow null for values 
  - Common API
    - V put(K key, V value)
    - V get(Object key) `使用object给user一个自由度，可以通过自己定义.equal来定义key是否相等`
    - V remove(Object key)
    - Boolean containsKey(Object key)
    - Set<Map.Entry<K, V>> entrySet() - get the set view of all the entries
    - Set<K> keySet(): get the set view of all the keys in hashmap
    - Collection<V> values(): get the collection view of all the values
    - bllean containsValue(Object value) - O(n)
    - Void clear()
    - int size()
    - Boolean isEmpty()
- TreeMap
- LinkedHashMap



hashtable vs hashmap

1. hashtable are synchronized, introduce a lot of performance penalty
2. hashtable does not allow null key,



Hashmap实现原理

- Collision:

  - Separate chaining: the element of each of the buckets is actually a single linked list.

    - 每次加在linkedlist的头，因为recent add 更大几率被访问

  - Open addressing: put the key-value pair into the "next" available bucket

    - how to define next? Linear/quadratic/exponential probing, hash again

    - challenge: handling removed keys in the map

    - not used by Java, but by some real life systems

    - 查找的时候

      case1: 一直找到空可以确认key不存在

      case2: 如果hash第一次不是想找的key, 我们按顺序往下找，直到找到

key.hashCode(): to determine the entry index for the key

Key.equals(): to determine whether two keys are the same keys

Hashmap 的性能很大一部分取决于key.hashCode()， 是否分布零散



java List里面不需要类型相同，只要size一样，并且每个值相等, .equal返回true

 hashcode 一般采取滚动hash, 常用31这个数



小trick

Set<String> 可以用代替写一个class并且需要override .equals 和 .hashcode 来去重



```
public class HashMap {
	private Entry[]array;
	private int size;
	private double loadFactor;
	
	public HashMap() {
	
	}
	
	public HashMap() {
	
	}
}

class Entry {
	String key;
	Integer value;
	Entry next;
	public Entry(String key, Integer value) {
		this.key = key;
		this.value = value;
		this.next = null;
	}
}
```



