## Collections

![](/notes/images/collections.jpg)

![](/notes/images/collections-complex.png)

||Hash Table|Resizable Array|Balanced Tree|Linked List|Hash Table + Linked List|
|-    |-|-|-|-|-|
|Set  |HashSet| 	  	   |TreeSet| 	  	    |LinkedHashSet
|List | 	  	|ArrayList |	  	 |LinkedList| 	 
|Deque| 	  	|ArrayDeque| 	  	 |LinkedList| 	 
|Map  |HashMap| 	  	   |TreeMap| 	  	    |LinkedHashMap

- Map
  - HashTable - хэш-таблица, не позволяет null в качестве ключа, все методы synchronized (низкая производительность)
  - HashMap - позволяет null в качестве ключа, не синхронизированна
  - LinkedHashMap - упорядоченная мапа, основанная на двухсвязном списке
  - TreeMap - упорядоченная мапа основанная на красно-черном дереве
  - WeakHashMap - мапа с слабыми ссылками, gc удалит объекты если на них не будет других ссылок.

- List
  - Vector - dynamic array. All methods are synchronized (low perfomance). Allows null object. Recomended to use `ArrayList`
  - Stack - LIFO. Partially synchronized (all except `push()`). Recomended to use `ArrayDeque`
  - ArrayList - dynamic array. Recomended when a lot of getting operations ( O(1) ).
  - LinkedList - bidirectional list. adding - O(1)

- Set
  - HashSet - внутри объект hashMap для хранения, элементы хранятся на месте ключа, а на место значения ложится new Object()
  - LinkedHashSet - использует LinkedHashMap для хранения, гарантирует порядок для вставки.
  - TreeSet - использует NavigableMap, поддерживает порядок при помощи Comparator

- Queue
  - LinkedList
  - PriorityQueue - natural sorted elements. Order can be overridden by additional `Comparator`
  - ArrayDeque - LIFO. dynamic array, doesn't allow null element and access by index.  
