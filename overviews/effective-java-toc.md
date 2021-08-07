---
description: 2016.08.19
---

# Effective Java TOC

The table of contents of the book [Effective Java by Joshua Bloch \(2nd edition, 2008\)](https://www.amazon.com/Effective-Java-2nd-Joshua-Bloch/dp/3). It is a good overview of the rules recommended by the book.

### Creating and Destroying Objects

* Consider static factory methods instead of constructors 
* Consider a builder when faced with many constructor parameters 
* Enforce the singleton property with a private constructor or an enum type 
* Enforce noninstantiability with a private constructor 
* Avoid creating unnecessary objects 
* Eliminate obsolete object references 
* Avoid finalizers 

### Methods Common to All Objects

* Obey the general contract when overriding equals 
* Always override hashCode when you override equals
* Always override toString 
* Override clone judiciously 
* Consider implementing Comparable 

### Classes and Interfaces

* Minimize the accessibility of classes and members 
* In public classes, use accessor methods, not public fields 
* Minimize mutability 
* Favor composition over inheritance 
* Design and document for inheritance or else prohibit it 
* Prefer interfaces to abstract classes 
* Use interfaces only to define types
* Prefer class hierarchies to tagged classes 
* Use function objects to represent strategies 
* Favor static member classes over nonstatic 

### Generics

* Don’t use raw types in new code 
* Eliminate unchecked warnings
* Prefer lists to arrays 
* Favor generic types
* Favor generic methods 
* Use bounded wildcards to increase API flexibility 
* Consider typesafe heterogeneous containers 

### Enums and Annotations

* Use enums instead of int constants
* Use instance fields instead of ordinals 
* Use EnumSet instead of bit fields 
* Use EnumMap instead of ordinal indexing
* Emulate extensible enums with interfaces 
* Prefer annotations to naming patterns 
* Consistently use the Override annotation
* Use marker interfaces to define types 

### Methods

* Check parameters for validity 
* Make defensive copies when needed 
* Design method signatures carefully 
* Use overloading judiciously 
* Use varargs judiciously 
* Return empty arrays or collections, not nulls 
* Write doc comments for all exposed API elements 

### General Programming

* Minimize the scope of local variables 
* Prefer for-each loops to traditional for loops 
* Know and use the libraries 
* Avoid float and double if exact answers are required 
* Prefer primitive types to boxed primitives 
* Avoid strings where other types are more appropriate 
* Beware the performance of string concatenation 
* Refer to objects by their interfaces 
* Prefer interfaces to reflection 
* Use native methods judiciously
* Optimize judiciously 
* Adhere to generally accepted naming conventions 

### Exceptions

* Use exceptions only for exceptional conditions 
* Use checked exceptions for recoverable conditions and runtime exceptions for programming errors 
* Avoid unnecessary use of checked exceptions 
* Favor the use of standard exceptions
* Throw exceptions appropriate to the abstraction
* Document all exceptions thrown by each method
* Include failure-capture information in detail messages 
* Strive for failure atomicity 
* Don’t ignore exceptions 

### Concurrency

* Synchronize access to shared mutable data
* Avoid excessive synchronization 
* Prefer executors and tasks to threads
* Prefer concurrency utilities to wait and notify
* Document thread safety 
* Use lazy initialization judiciously 
* Don’t depend on the thread scheduler 
* Avoid thread groups 

### Serialization

* Implement Serializable judiciously
* Consider using a custom serialized form 
* Write readObject methods defensively 
* For instance control, prefer enum types to readResolve 
* Consider serialization proxies instead of serialized instances

