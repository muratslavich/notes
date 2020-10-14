## References

1. Strong References
2. Weak References
3. Soft References
4. Phantom References

### Strong References
This is the default type/class of Reference Object. Any object which has an active strong reference are not eligible for garbage collection. The object is garbage collected only when the variable which was strongly referenced points to null.

### Weak References 
Weak Reference Objects are not the default type/class of Reference Object and they should be explicitly specified while using them.
- This type of reference is used in `WeakHashMap` to reference the entry objects.
- If JVM detects an object with only weak references (i.e. no strong or soft references linked to any object object), this object will be marked for garbage collection.
- To create such references `java.lang.ref.WeakReference` class is used.
- These references are used in real time applications while establishing a DBConnection which might be cleaned up by Garbage Collector when the application using the database gets closed.

### Soft References
In Soft reference, even if the object is free for garbage collection then also its not garbage collected, until JVM is in need of memory badly.The objects gets cleared from the memory when JVM runs out of memory.To create such references `java.lang.ref.SoftReference` class is used.

### Phantom References
The objects which are being referenced by phantom references are eligible for garbage collection. But, before removing them from the memory, JVM puts them in a queue called ‘`reference queue`’ . They are put in a reference queue after calling `finalize()` method on them.To create such references `java.lang.ref.PhantomReference` class is used
