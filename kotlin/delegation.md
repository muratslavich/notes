## Delegation pattern
OOP pattern when object handles a request by delegating to a second object - the delegate.

```Java
class RealPrinter {
    void print() { System.out.println("The delegate"); }
}

class Printer {
    RealPrinter printer = new RealPrinter();

    void print() { printer.print(); }
}
```

The delegation pattern is the good alternative to implementation inherritance.

Kotlin support it natively

```Java
interface Base {
    fun print()
}

class BaseImpl(val x: Int) : Base {
    override fun print() { print(x) }
}

class Derived(b: Base) : Base by b

// override delegate functional
class Derived(b: Base) : Base by b {
    override fun print() { print("abc") }
}

fun main() {
    val b = BaseImpl(10)
    Derived(b).print()
}
```
