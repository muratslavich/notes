##  Innner classes

![](/notes/images/inner_classes.jpg)

### Inner class
You just need to write a class within a class.

> private inner cannot be accessed from an object outside the class.

```java
class Outer {
  public void display() {
    Inner inner = new Inner();
    inner.print();
  }

  private class Inner {
    public void print() { println("Inner"); }
  }
}

public static void main() {
  Outer outer = new Outer();
  outer.display();

  // if inner class public we can instantiate inner class
  Outer_Demo.Inner_Demo inner = outer.new Inner_Demo();
}
```
### Method-local inner class
A method-local inner class can be instantiated only within the method where the inner class is defined.

```java
class Outer {
  void method() {
    // method-local inner class
    class MethodInner_Demo {
      public void print() {
        System.out.println("This is method inner class "+num);	   
      }   
    } // end of inner class

    // Accessing the inner class
    MethodInner_Demo inner = new MethodInner_Demo();
    inner.print();
  }
}
```

### Anonymous Inner class
Declare and instantiate them at the same time

> if a method accepts an object of an interface, an abstract class, or a concrete class, then we can implement the interface, extend the abstract class, and pass the object to the method. If it is a class, then we can directly pass it to the method.

```java
AnonymousInner an_inner = new AnonymousInner() {
   public void my_method() {
      ........
      ........
   }   
};
```

### Static nested classes

> A static inner class is a nested class which is a static member of the outer class. It can be accessed without instantiating the outer class, using other static members. Just like static members, a static nested class does not have access to the instance variables and methods of the outer class.

```java
class MyOuter {
   static class Nested_Demo {
   }
}
```
