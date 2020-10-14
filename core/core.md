# Java Core

|Type   |Default|Size   |Range
|-------|-------|-------|-----
|boolean|false  |1 bit  |
|char   |\u0000 |16 bit |\u0000 - \uFFFF
|byte   |0      |8 bit  |-128 to 127
|short  |0      |16 bit |-32,768 to 32,767
|int    |0      |32 bit |-2*10^9 to 2*10^9
|long   |0      |64 bit |-9*10^18 to 9*10^18
|float  |0.0    |32 bit |upto 7 decimal digits
|double |0.0    |64 bit |upto 16 decimal digits

![](/notes/images/type-conv.png)

![](/notes/images/boxing.jpg)

|Object class methods|Description|
|-|-|
|boolean equals( Object o )| 	Gives generic way to compare objects|
|Class getClass()| 	The Class class gives us more information about the object|
|int hashCode()| 	Returns a hash value that is used to search objects in a collection|
|void notify()| 	Used in synchronizing threads|
|void notifyAll()| 	Used in synchronizing threads|
|String toString()| 	Can be used to convert the object to String|
|void wait()| 	Used in synchronizing threads|
|protected Object clone() throws CloneNotSupportedException| 	Return a new object that are exactly the same as the current object|
|protected void finalize() throws Throwable| 	This method is called just before an object is garbage collected|
