---

title: Patterns
layout: page
header-img: "img/pattern-blue.jpg"

---

# Design Patterns

> "Each pattern describes a problem which occurs over and over again in our environment, and then describes the core of the solution to that problem, in such a way that you can use this solution a million times over, without ever doing it the same way twice"
> 
> _Christopher Alexander_
>
> A Pattern is a solution to a problem in a context.

---

### Strategy;
Defines a family of algorithms encapsulates each one, and make them interchangeable.
Strategy lets the algorithm vary independetly from clients that use it.

---

### Observer;
Defines a one-to-many dependency between objects so that when one object changes state, all it's dependents are notified and updated automatically.

---

### Decorator;
Attaches additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.

---

### Factory Method;
Define an interface for creating an object, but lets subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

---

### Abstract Factory;
Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

---

### Singleton;
Ensures a class has only one instance, and provides a global point of access to it.

--

### Command;
Encapsulates a request as an object, thereby letting you parameterize other objects with different requests, queue or log requests, and support undoable operations.

---

### Adapter;
Converts the interface of a class into another interface the clients expects. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.

---

### Facade;
Provides an unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.

---

### Template Method;
Defines the skeleton of an algorithm in a method, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.

---

### Iterator;
Provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

---

### Composite;
Allows you to compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.

---

### State;
Allows an object to alter its behavior when its internal state changes. The object will appear to change its class.

---

### Proxy;
Provides a surrogate or placeholder for another object to controll access to it.

---

### Builder;
Separate the construction of a complex object from its representation allowing the same construction process to create various representations.

---

### Prototype;
Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.

---

### Compound Patterns;
A Compound Pattern combines two or more patterns into a solution that solves a recurring or general pattern.

#### MVC;
The MVC is a compound pattern consisting of the Observer, Strategy and Composite patterns.

---

### Messaging Patterns
A Messaging Pattern is a network-oriented architectural pattern which describes how two different parts of a message passing system connect and communicate with each other.

#### Request - Reply

#### Publish - Subscribe

#### Push - Pull

#### Exclusive pair

---
