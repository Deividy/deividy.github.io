---

layout: default
title: A few words about GRASP
comments: true

---

# A few words about GRASP

GRASP = General Responsibility Assignment Software Patterns

 - The critical design tool for software development is a mind well educated in design principles. It is not the UML or any other technology.

 - What's been done?
 - How do things relate?
 - How much design modeling to do, and how?
 - What's the output

**RDD - Responsibilities and Responsiblity-Driven Design**

#### Doing responsibilities of an object:
 - doing something itself, such as creating an object or doing a calculation
 - initiating action in other objects
 - controlling and coordinating activities in other objects

#### Knowing responsibilities of an object:
 - knowing about private encapsulated date
 - knowing about related objects
 - knowing about things it can derive on calculate

 RDD is a general metaphor for thinking about OO software design. Think of software objects as similar to people with responsibilities who collaborate with other people to get work done. RDD leads to viewing an OO design as a community of collaborating responsible objects.
 
### What are Patterns?
In OO design, a pattern is a named description of a problem and solution that can be applied to new contexts; ideally, a pattern advises us on how to apply its solution in varying circumstances and considers the forces and trade-offs.

Most simply, a good pattern is a named and well-known problem/solution pair that can be applied in new contexts, with advice on how to apply it in novel situations and discussion of its trade-offs, implementations, variations, and so forth.

### Patterns have NamesImportant!
 - It supports chunking and incorporating that concept into our understanding and memory.
 - It facilitates communication.

<!--break-->

#### GRASP - General Responsibility Assignment Software Patterns
 - Creator
 - Infromation Expert
 - Low Coupling
 - Controller
 - High Cohesion

 - Indirection
 - Polymorphism
 - Protected Variations
 - Pure Fabrication

(Solution / Advice)

#### Creator
 Name:      Creator
 Problem:   Who creates an A?
 Solution:  Assign class B the responsibility to create an instance of class A if one of these is true (the more better)
  - B 'contains' or compositely aggregates A.
  - B records A.
  - B closely uses A.
  - B has the initializing data for A.

#### Information Expert
 Name:      Information Expert
 Problem:   What is a basic principle by which to assign responsibilities to object?
 Solution:  Assign a responsibility to the class that has the information needed to fulfill it.


#### Low Coupling
 Name:      Low Coupling
 Problem:   How to reduce the impact of change?
 Solution:  Assign responsibilities so that (unnecessary) coupling remains low. Use this principle to evalute alternatives.

#### Controller
 Name:      Controller
 Problem:   What first object beyond the UI layer receveis and coordinates ("controls") a system operation?
 Solution:  Assign the responsibility to an object representing one of these choices:
   - Represents the overall "system", a "root object", a device that the software is running within, or a major subsystem
   -Represents a use case scenario within which the system operation occurs

#### High Cohesion
 Name:      High Cohesion
 Problem:   How to keep objects focused, understandable, and manageable, and as a side effect, support Low Coupling?
 Solution:  Assign responsibilities so that cohesion remains high. Use this to evalute alternatives.


