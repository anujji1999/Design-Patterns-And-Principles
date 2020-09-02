# Design Patterns and Principles
**A collection of design patterns and principles written in Kotlin.**

### Design Principles

* **Identify the aspects of your application that vary and separate them from what stays the same.** Take the parts that vary and encapsulate them, so that later you can alter or extend the parts that vary without affecting those that don’t.

* **Program to an interface, not an implementation.** "Program to an interface" really means "Program to a supertype". The word interface is overloaded here. There’s the concept of interface, but there’s also the Java construct interface. You can program to an interface, without having to actually use a Java interface. The point is to exploit polymorphism by programming to a supertype so that the actual runtime object isn’t locked into the code.

* **Favor composition over inheritance.** Creating systems using composition gives you a lot more flexibility. Not only does it let you encapsulate a family of algorithms into their own set of classes, but it also lets you change behavior at runtime as long as the object you’re composing with implements the correct behavior interface.

* **Strive for loosely coupled designs between objects that interact.** Loosely coupled designs allow us to build flexible OO systems that can handle change because they minimize the interdependency between objects.

* **The Open-Closed Principle: Classes should be open for extension, but closed for modification.** Allow classes to be easily extended to incorporate new behavior without modifying existing code. Such designs are resilient to change and flexible enough to take on new functionality to meet changing requirements. While it may seem like a contradiction, there are techniques for allowing code to be extended without direct modification. Be careful when choosing the areas of code that need to be extended; applying the Open-Closed Principle EVERYWHERE is wasteful and unnecessary, and can lead to complex, hard-to-understand code.

* **Dependency Inversion Principle: Depend upon abstractions. Do not depend upon concrete classes.** At first, this principle sounds a lot like “Program to an interface, not an implementation,” right? It is similar; however, the Dependency Inversion Principle makes an even stronger statement about abstraction. It suggests that our high-level components should not depend on our low-level components; rather, they should both depend on abstractions. A “high-level” component is a class with behavior defined in terms of other, “low-level” components. For example, [PizzaStore](src/factorymethod/pizzastoreexample/pizzastore/PizzaStore.kt) is a high-level component because its behavior is defined in terms of pizzas - it creates all the different pizza objects, and prepares, bakes, cuts, and boxes them, while the pizzas it uses are low-level components.

    _**Where’s the “inversion” in Dependency Inversion Principle?**_
    
    The “inversion” in the name Dependency Inversion Principle is there because it inverts the way you typically might think about your OO design. The low-level components depend on a higher level abstraction. Likewise, the high-level component is also tied to the same abstraction. So, the top-to-bottom dependency chart has inverted itself, with both high-level and low- level modules now depending on the abstraction.

### Design Patterns

* **Strategy Pattern:** The Strategy Pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. Strategy lets the algorithm vary independently of clients that use it.
  * **Example:** [An action game design using Strategy pattern](https://github.com/Devansh-Maurya/Design-Patterns-And-Principles/tree/master/src/strategy/actiongame)
  
* **Observer Pattern: The Observer Pattern defines a one-to-many dependency between objects so that when one object changes state, all of its dependents are notified and updated automatically.** Subjects, or as we also know them, Observables, update Observers using a common interface. Observers are loosely coupled in that the Observable knows nothing about them, other than that they implement the Observer interface. You can push or pull data from the Observable when using the pattern (pull is considered more “correct”). Don’t depend on a specific order of notification for your Observers. Java has several implementations of the Observer Pattern, including the general purpose java.util.Observable.
  * **Example:** Weather app design using Observer pattern.
     1. [From scratch](https://github.com/Devansh-Maurya/Design-Patterns-And-Principles/tree/master/src/observer/weatherdata/scratch)
     2. [Using Java's in-built Observer pattern](https://github.com/Devansh-Maurya/Design-Patterns-And-Principles/tree/master/src/observer/weatherdata/inbuilt)

* **Decorator Pattern: The Decorator Pattern attaches additional responsibilities to an object dynamically.Decorators provide a flexible alternative to subclassing for extending functionality.** Composition and delegation can often be used to add new behaviors at runtime. The Decorator Pattern provides an alternative to subclassing for extending behavior. The Decorator Pattern involves a set of decorator classes that are used to wrap concrete components. Decorator classes mirror the type of the components they decorate. (In fact, they are the same type as the components they decorate, either through inheritance or interface implementation.) Decorators change the behavior of their components by adding new functionality before and/or after (or even in place of) method calls to the component. You can wrap a component with any number of decorators. Decorators are typically transparent to the client of the component; that is, unless the client is relying on the component’s concrete type. Decorators can result in many small objects in our design, and overuse can be complex.
  * **Example:** [Making different beverages with add-ons using Decorator pattern](https://github.com/Devansh-Maurya/Design-Patterns-And-Principles/tree/master/src/decorator/coffeeshop)
