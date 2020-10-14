### Immutability

#### Disadvantages
- Mutable objects `allows mutating` throughout methods parameters
- `Void return` type and `mutate inside` - design problem
- Allow to distribute and complicate object creation throughout code
- Don't well in multithreading - possibility for `race conditions`

#### How make immutable class
- Make all fields final
- Define constructor
- Remove setters
- Use `@With` instead of `@Setter`

```java
public class WithExample {
  private @NonNull final String name;
  private final int age;

  public WithExample(String name, int age) {
    if (name == null) throw new NullPointerException();
    this.name = name;
    this.age = age;
  }

  protected WithExample withName(@NonNull String name) {
    if (name == null) throw new java.lang.NullPointerException("name");
    return this.name == name ? this : new WithExample(name, age);
  }

  public WithExample withAge(int age) {
    return this.age == age ? this : new WithExample(name, age);
  }
```

#### Immutable in java

[habr](https://habr.com/en/company/piter/blog/470149/)

> In java it doesnt exist immutable collections at all. Java 9 brings `Collections.unmodifiableCollection(list)` a wrapper over the common collections which throw `UnsupportedOperationException` over mutation methods


#### Immutable in Kotlin

![](/notes/images/kotlin-immutable.png)
