### Equals and HashCode

#### Equality - objects of the same class with equal fields
- reflexive: `a.equals(a) == True`
- symmetric: `x.equals(y) == y.equals(x)`
- transitive: if `x.equals(y)` and `y.equals(z)` -> `x.equals(z)`
- consistent: result of equality changes only if some field has changed

>Thus, if we override the equals() method, we also have to override hashCode().

#### Hash - function that map object to fixed size value
- Internal consistency: `hashCode()` changes only if a related with `equals()` field has changed
- equals consistency: if `a.eqauls(b) == True` -> `a.hashCode() == b.hashCode()`
- collisions: if `a.eqauls(b) == False` -> it can be the same hashes
 <br/>
 
### equals() implementation

`==          `-> compares identity, or reference equality.  
`equals()    `-> compares object states (object data).  

###### Default equals() implementation in Class Object
> Shallow comparison: The default implementation of equals method simply checks if two objects references refer to the same Object.

```java
public boolean equals(Object obj) {
    return (this == obj);
}
```
<br/>

###### Rules
- Object fields and collections : use equals
- enums : equals or == (same for enums)
- nullable object : use both equals and ==
- array fields : use Arrays.equals(first, second)
- primitives : use ==
- float and doubles : convert to (int) and use ==
- use order for comparing && - short-circuit logical operation
- be careful extending class with equals implementation - if you add new fields which contributes to equality.

```java
// class Money
@Override
public boolean equals(Object o) {
    if (o == this)
        return true;
    if (!(o instanceof Money))
        return false;
    Money other = (Money)o;
    boolean currencyCodeEquals = (this.currencyCode == null && other.currencyCode == null)
      || (this.currencyCode != null && this.currencyCode.equals(other.currencyCode));
    return this.amount == other.amount && currencyCodeEquals;
}
```

  
> It can violations happen, if we extend a class that has overridden equals().

```java
/** class Money
*   class WrongVoucher extend Money
*/

Money cash = new Money(42, "USD");
WrongVoucher voucher = new WrongVoucher(42, "USD", "Amazon");

voucher.equals(cash) => false // As expected.
cash.equals(voucher) => true // That's wrong.
```
<br/>
  
### hashCode() implementation
##### Default hashCode()
`public native int hashCode();` - Depend on JVM. In OpenJdk.
- В версиях 6 и 7 это случайно генерируемое число.
- В версиях 8 и 9 это число, полученное на основании состояния потока.
- Azul’s Zing действительно генерирует идентификационный хеш на основании адреса памяти объекта.

```java
public class User {
    private int id;
    private String name;
    private String email;
}
```
<br/>

This implementation also agreed to the respective contract, but all algorithms who use hash code would be degraded.    
For example in HashMap all object would be stored in one bucket.  
```java
@Override
public int hashCode() {
    return 1;
}
```
<br/>
  
For different hash for unequal objects we have to consider all fields of the class.  
```java
@Override
public int hashCode() {
    return (int) id * name.hashCode() * email.hashCode();
}
```
<br/>
  
Standard implementation.  
To get more unique hashes we can use prime numbers (31 here).  
31 - простое, нечетное число, умножение на которое заменяется компилятором автоматически на (n << 5) - n = n * 31.  
Умножение на четное число может привести к переполнению hash числа и информация будет потеряна.  
От этого зависит распределение хэш функции.  
```java
@Override
public int hashCode() {
    int hash = (int) (id ^ (id >>> 32));
    hash = 31 * hash + (name == null ? 0 : name.hashCode());
    hash = 31 * hash + (email == null ? 0 : email.hashCode());
    return hash;
}
```
<br/>
  
> Хэш от числа int - само число

<br/>
  
Как взять хэш от long. `int hash = (int) (id ^ (id >>> 32));`  
Беззнаковый сдвиг вправо на 32 бита - то есть мы берем старшие биты.  
XOR числа на полученное ранее значение - по сути XOR старших битов с младшими.  
Это необходимо потому что при округление до int, все биты старше 32 будут отброшены.  
Это обеспечиват вклад старших битов в конечный хэш.  
```
01010101010101010101010101010101 0001 1111 0001 0001 0001 1111 0001 0001 >> 32     // 6 148 914 690 326 077 201 xor
00000000000000000000000000000000 0101 0101 0101 0101 0101 0101 0101 0101           //             1 431 655 765

01010101010101010101010101010101 0100 1010 0100 0100 0100 1010 0100 0100           // 6 148 914 691 050 850 884 (int)
                                 0100 1010 0100 0100 0100 1010 0100 0100           //             1 245 989 444 
```
<br/>
  
String.hashCode() compute as:  
> каждый символ умножается на 31^(n-1)
```
s[0]*31^(n-1) + s[1]*31^(n-2) + ... + s[n-1]
```
