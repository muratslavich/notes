### HashMap
- [Initialization](#initialization)
- [Adding element](#adding-element)
- [Getting value](#getting-element)
- Removing element
- Resize
- Iteration

#### HashMap

```java
public class HashMap<K,V> implements Map<K,V> {
    Node<K,V>[] table;  // массив - хранилище ссылок на цепочки значений
    Set<Map.Entry<K,V>> entrySet; // хранилище связок (entry) ключ - значение
    int size;           // 16 by default
    int threshold;      // Предельное количество элементов, при достижении которого, размер хэш-таблицы увеличивается вдвое. `(capacity * loadFactor)`
    float loadFactor;   // Коэффициент загрузки. Значение по умолчанию 0.75
}

class Node<K,V> implements Map.Entry<K,V> {
    final int hash;
    final K key;
    V value;
    Node<K,V> next;
}
```

![](/notes/images/hash-map.png)
<br/>

#### Initialization
HashMap defines `initialCapacity` and `loadFactor` during initialization.

<details>
<summary>Examples</summary>

##### Static map initialization
```java
public static Map<String, String> articleMapOne;
static {
    articleMapOne = new HashMap<>();
    articleMapOne.put("ar01", "Intro to Map");
    articleMapOne.put("ar02", "Some article");
}
```

##### Double quote initialization
>it creates an anonymous extra class at every usage, holds hidden references to the enclosing object, and might cause memory leak issues

```java
Map<String, String> doubleBraceMap  = new HashMap<String, String>() {
    { put("key1", "value1"); put("key2", "value2"); }
};
```

##### Using Collections
> Collections return unmodifiableCollection

```java
Map<String, String> map = Collections.singletonMap("", "");
Map<String, String> map = Collections.emptyMap();
```

##### Using stream

```java
Map<String, String> map = Stream.of(new String[][] {
  { "Hello", "World" },
  { "John", "Doe" },
}).collect(Collectors.toMap(data -> data[0], data -> data[1]));

Map<String, Integer> map = Stream.of(new Object[][] {
  { "data1", 1 },
  { "data2", 2 },
}).collect(Collectors.toMap(data -> (String) data[0], data -> (Integer) data[1]));

Map<String, Integer> map = Stream.of(
  new AbstractMap.SimpleEntry<>("idea", 1),
  new AbstractMap.SimpleEntry<>("mobile", 2)
).collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));

Map<String, Integer> map = Stream.of(
  new AbstractMap.SimpleImmutableEntry<>("idea", 1),    
  new AbstractMap.SimpleImmutableEntry<>("mobile", 2)
).collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));
```

##### Java 9

```java
Map<String, String> emptyMap = Map.of();
Map<String, String> singletonMap = Map.of("key1", "value");
Map<String, String> map = Map.of("key1","value1", "key2", "value2");

Map<String, String> map = Map.ofEntries(
  new AbstractMap.SimpleEntry<String, String>("name", "John"),
  new AbstractMap.SimpleEntry<String, String>("city", "budapest"),
  new AbstractMap.SimpleEntry<String, String>("zip", "000000"),
  new AbstractMap.SimpleEntry<String, String>("home", "1231231231")
);
```

</details>

#### Adding element

```java
someMap.put("key", value);
```

> Computes key.hashCode() and spreads (XORs) higher bits of hash to lower.  
> because the table use _power-of-two masking_ to get `index = hash & (n-1)`, n - table size  
> --  
> Power of two masking  
> for example we have int hash 1141113916, but table size - 16  
> 0100 0100 0000 0100 0000 0100 0011 1100 &  
> 0000 0000 0000 0000 0000 0000 0000 1111  
> 0000 0000 0000 0000 0000 0000 0000 1100 - 12
1. hash(key)
    - `if (key == null) return 0`
    - `else (hash = key.hashCode()) ^ (hash >>> 16)` 
2. find index `i = (n - 1) & hash`
3. crete Node `new Node { hash = 1256; key=key; value=value; next=null }`
4. put created node to table with index 
    - if bucket is empty `table[i] = node`
    - else check each key to `existKey.hashCode == newKey.hashCode && newKey.equals(existKey)` if True -> replace node
    - else put in the end of the nodes list (previous next reference set to new node) 
> In java 8 and newer, after certain number of collision, list replaced by balanced Tree
> O(log n) in the worst case instead of O(n) with lists

#### Getting element
1. hash(key)
2. table index
3. iterate to all entries and check keys to `existKey.hashCode == newKey.hashCode && newKey.equals(existKey)`
4. if next element == null; return null