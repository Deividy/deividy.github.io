---

title: Design Principles
layout: default

---

# Design Principles

#### Encapsulate what varies.
Identify the aspects of your application that vary and separate them from what stays the same.
Take what varies and "encapsulate" it so it won't affect the rest of your code.

---

#### Favor composition over inheritance.

--

#### Program to interfaces, not implementation.

---

#### Strive for loosely coupled designs between objects that interact.

---

#### Classes open for extension, but closed for modification.

---

### Dependency Inversion Principle
**Depend upon abstractions. Do not depend upon concrete classes**
- No variable should hold a reference to a concrete class.
- No class should derive from a concrete class.
- No method should override an implemented method of any of its based classes.