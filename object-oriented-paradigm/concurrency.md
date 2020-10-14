# [Design patterns](patterns.md)
## Concurrency
##### Double-checked locking

<details><summary> useful links </summary>  

[Ещё раз (надеюсь, последний) про double-checked locking](https://habr.com/en/post/248041/)  
[Реализация Singleton в JAVA](https://habr.com/en/post/27108/)  
[Правильный Singleton в Java](https://habr.com/en/post/129494/)  
[А как же всё-таки работает многопоточность? Часть II: memory ordering](https://habr.com/en/post/209128/)  
</details>


<details>
<summary> code</summary>

> It isn't working in multithreading program.
Because two threads can refer to getHelper() and while the first thread creates an object the second can already create it.

```java
class Foo {
    private Helper helper = null;

    public Helper getHelper() {
        if (helper == null)
            helper = new Helper();
        return helper;
    }
}
```

> It's working but synchronized method will add overhead in each calling.
When thread only reads property, having entire method synchronization is excessive.

```java
class Foo {
    private Helper helper = null;

    public synchronized Helper getHelper() {
        if (helper == null)
            helper = new Helper();
        return helper;
    }
}
```

> If the object has been initialized, locking won't be used. But while the thread is trying to get locking, the object can be initialized already. For this, there is use double-check lock after getting locking object.

```java
class Foo {
    private Helper helper = null;

    public Helper getHelper() {
        if (helper == null) {
            synchronized(this) {
                if (helper == null) {
                    helper = new Helper();
                }
            }
        }
        return helper;
    }
}
```

> There is another issue. While the first thread gets locking and trying to initialize the object, the second thread can consider that object already exists and if he tries to use it before the first thread will finish initialization, it may be the NPE reason. Volatile makes it possible to correct write in this case

Also [volatile](http://tutorials.jenkov.com/java-concurrency/volatile.html)

```java
class Foo {
    private volatile Helper helper = null;

    public Helper getHelper() {
        if (helper == null) {
            synchronized(this) {
                if (helper == null) {
                    helper = new Helper();
                }
            }
        }
        return helper;
    }
}
```

</details>

##### Monitor Object
##### Read write lock pattern
##### Scheduler pattern
##### Thread pool pattern
