---
description: 2016.06.19
---

# What Is The Problem With Abstract Frameworks?

I often find it very hard to maintain the class hierarchies we write. And I am constantly thinking about the reasons, why. Inheritance is one of the basic principles of object-oriented programming, so it may sound strange that there is a problem with it. Of course, inheritance is good but the way we use it may not be good. Let me explain it through an example.

### Feature development

Imagine that you are a programmer and you have a task to implement a certain feature. What do you expect?

Specification:

* The feature is carefully found out and discussed by one or more business analysts.

Design:

* Prior to the coding, the solution is well planned by technical people like architects or by the developers themselves. At least verbally but possibly in written documents.

Implementation:

* The feature is not only implemented well, but it also _fulfills the requirements_.

Test:

* The implemented program is tested on at least one level but more levels are better \(unit, functional, integration, etc. tests\).

Usually, these steps happen in a software company.

### Framework development

When you create class hierarchies to use them in the future, and to use them by other developers, then you really create a _**framework**_. Especially the presence of abstract classes shows that others have to _"put their classes under this hierarchy"_, i.e. implement classes and methods. That is what I call a _"framework"_.

So imagine now that you have to implement a framework. Wouldn't you expect the same conditions as in the feature development?

* Specification
* Design
* Implementation
* Testing

Yes, you would.

### Inheritance in reality

And now let's see how and why programmers create class hierarchies and abstract classes in reality. They work on a certain feature and create classes for it. During the coding they might say:

> "It is so generic, I extract it to a parent class."

Or, even more often they discover the similarities between some classes and they say:

> "I put the equal parts into a common base class and the differences into abstract methods."

Or they may have other complex reasons including the usage of a design pattern \(which is at least a more judicious approach\).

But remember, this is a framework development. What about the expected conditions?

* Specification: _No_
* Design: _No_
* Implementation: _Yes but..._
* Testing: _No_

A little bit more detailed:

Specification:

* The intention of such frameworks is always this one:

  > "It will be good for the next developer / modification / sub-class / etc."

* But unfortunately, it will not.

Design:

* There is only an _**ad hoc**_ design. The programmer has just a quick idea, which usually does not exceed the _"common base class"_ antipattern.
* Moreover, it does not fulfill the specification. \(Remember: _"It is generic."_ or _"It will be good for the future."_\). Instead of that, it usually only freezes the differences between some already existing specific classes.

Implementation:

* There is, but not in the terms of fulfilling the requirements since there are none.

Testing:

* The developers usually test only the sub-classes, which involves more or less the code from the parent classes too. But the parent classes - especially the abstract ones - are not explicitly tested. They are not tested like any other classes with a well-defined and enclosed functionality.

