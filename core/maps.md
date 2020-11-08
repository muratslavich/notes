## Maps

### HashMap
- [Initialization](#initialization)
- Adding element
- Resize
- Removing element
- Iteration

#### HashMap

- __table__ — Массив типа `Entry[]`, который является хранилищем ссылок на списки (цепочки) значений;
- __loadFactor__ — Коэффициент загрузки. Значение по умолчанию 0.75 является хорошим компромиссом между временем доступа и объемом хранимых данных;
- __threshold__ — Предельное количество элементов, при достижении которого, размер хэш-таблицы увеличивается вдвое. Рассчитывается по формуле `(capacity * loadFactor)`;
- __size__ — Количество элементов HashMap-а;

#### Initialization


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

