#### Basic principles
- Encapsulation - keeps realization inside and private, but provide public interface
- Inheritance - deriving some functional from parent class. Child extend base class. Relate as is.
- Polymorphism - many realization of one class can be used in one way by base class.

#### Diamond problem of multiple Inheritance
![](/notes/images/diamond.png)

#### Design principles
- SOLID
	- Single responsibility
	- Open for extension and close for modification
	- Liskov substitution principle - objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program.
	- Interface segregation principle
	- Dependency inversion principle - High-level modules should not depend on low-level modules. Dependency injection pattern solve this problem.

- DRY - Don't repeat yourself
- YAGNI - You ain't gonna need it
- KISS - keep it stupid simple
- GRASP - General Responsibility Assignment Software Patterns
	- Controller
	- Creator
	- Indirection
	- Information expert
	- High cohesion and low coupling
	- Polymorphism
	- Protected variations
	- Pure fabrication

- ACID
	- Atomic
	- Consistency - any data written to the database must be valid
	- Isolation - ensures that concurrent execution of transactions leaves the database in the same state that would have been obtained if the transactions were executed sequentially
	- Durability - guarantees that once a transaction has been committed, it will remain committed even in the case of a system failure
- CQRS - Command–query separation is a principle of imperative computer programming.

- High cohesion and low coupling
  - low coupling - How much do your different modules depend on each other?
  - high cohesion - represents the degree to which a part of a code base forms a logically single, atomic unit.


- Наследование - является
- Ассоциация - имеет
    - композиция - не существует вне
    - агрегация - внедряется извне
