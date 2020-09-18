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

* **Factory Method Pattern: The Factory Method Pattern defines an interface for creating an object, but lets subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.** As with every factory, the Factory Method Pattern gives us a way to encapsulate the instantiations of concrete types. The abstract Creator gives you an interface with a method for creating objects, also known as the “factory method.” Any other methods implemented in the abstract Creator are written to operate on products produced by the factory method. Only subclasses actually implement the factory method and create products. As in the official definition, you’ll often hear developers say that the Factory Method lets subclasses decide which class to instantiate. They say “decide” not because the pattern allows subclasses themselves to decide at runtime, but because the creator class is written without knowledge of the actual products that will be created, which is decided purely by the choice of the subclass that is used.
  * **Example:** [PizzaStore creating Pizzas using Factory method pattern](src/factorymethod/pizzastoreexample)
  
* **Abstract Factory Pattern: The Abstract Factory Pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes.** Abstract Factory allows a client to use an abstract interface to create a set of related products without knowing (or caring) about the concrete products that are actually produced. In this way, the client is decoupled from any of the specifics of the concrete products. Often the methods of an Abstract Factory are implemented as factory methods. The job of an Abstract Factory is to define an interface for creating a set of products. Each method in that interface is responsible for creating a concrete product, and we implement a subclass of the Abstract Factory to supply those implementations. So, factory methods are a natural way to implement your product methods in your abstract factories.
  * **Example:** [PizzaStore creating Pizzas with different ingredients using Abstract Factory pattern](src/abstractfactory/pizzastoreexample)
  
* **Singleton Pattern: The Singleton Pattern ensures a class has only one instance, and provides a global point of access to it.** We’re taking a class and letting it manage a single instance of itself. We’re also preventing any other class from creating a new instance on its own. To get an instance, we have to go through the class itself. We’re also providing a global access point to the instance: whenever you need an instance, just query the class and it will hand you back the single instance. We can implement this so that the Singleton is created in a lazy manner, which is especially important for resource-intensive objects.
  * **Example:**
      1. [From scratch](src/singleton/scratch)
      2. [Using Kotlin's `object`](src/singleton/kotlinobject)
      
* **Command Pattern: The Command Pattern encapsulates a request as an object, thereby letting you parameterize other objects with different requests, queue or log requests, and support undoable operations.** A **command object** encapsulates a request by binding together a set of actions on a specific **receiver**. To achieve this, it packages the actions and the receiver up into an object that exposes just one method, `execute()`. When called, `execute()` causes the actions to be invoked on the receiver. From the outside, no other objects really know what actions get performed on what receiver; they just know that if they call the `execute()` method, their request will be serviced. The examples linked below show parameterizing an object with a command. An **invoker** makes a request of a Command object by calling its `execute()` method, which invokes those actions on the receiver. Invokers can be parameterized with Commands, even dynamically at runtime. When commands support undo, they have an `undo()` method that mirrors the `execute()` method. Whatever `execute()` last did, `undo()` reverses. **Macro Commands** are a simple extension of Command that allow multiple commands to be invoked. Likewise, Macro Commands can easily support `undo()`. Commands may also be used to implement logging and transactional systems.
  * **Example:** A configurable remote control performing its actions using command objects
      1. [Without undo on invoker](src/command/RemoteLoader.kt)
      2. [With undo on invoker](src/command/RemoteLoaderWithUndo.kt)
      
* **Facade Pattern: The Facade Pattern provides a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.** To use the Facade Pattern, we create a class that simplifies and unifies a set of more complex classes that belong to some subsystem. Unlike a lot of patterns, Facade is fairly straightforward.
  * **Example:** [Home Theater system's interface simplified by using a Facade pattern](src/facade/hometheaterexample)