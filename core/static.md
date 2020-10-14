## Static keyword

Static in java
- Static Block
- Static Field
- Static Method
- Static Classes

> Basically, static is used for a constant variable or a method that is same for every instance of a class.

#### Static field
If a field is declared static, then exactly a single copy of that field is created and shared among all instances of that class.
From the memory perspective, static variables go in a particular pool in JVM memory called `Metaspace` (before Java 8, this pool was called `Permanent Generation` or `PermGen`, which was completely removed and replaced with `Metaspace`).

When use static field
- variable is independent of objects
- value is supposed to be shared across all objects

#### Static methods
Also belong to a class instead of the object, can be called without creating the object of the class.

When use static methods
- To access/manipulate static variables and other static methods that don't depend upon objects
- static methods are widely used in utility and helper classes

Should remember
- static methods can't be overridden
- abstract methods can't be static
- static methods cannot use this or super keywords
- static methods cannot access instance variables and instance methods directly

#### Static blocks
A static block is used for initializing static variables.

#### Static classes
Only nested classes can be static.
- static nested classes
- non-static are called inner classes

>The main difference between these two is that the inner classes have access to all member of the enclosing class (including private), whereas the static nested classes only have access to static members of the outer class.

In fact, static nested classes behaved exactly like any other top-level class but enclosed in the only class which will access it, to provide better packaging convenience.

> static nested classes do not have access to any instance members of the enclosing outer class; it can only access them through an object's reference

When use static classes

- Grouping classes that will be used only in one place increases encapsulation
- The code is brought closer to the place that will be only one to use it; this increases readability and code is more maintainable
- If nested class doesn't require any access to it's enclosing class instance members, then it's better to declare it as static because this way, it won't be coupled to the outer class and hence will be more optimal as they won't require any heap or stack memory
