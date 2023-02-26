---
description: 2023.02.26
---

# Simple Code Overview

<figure><img src="../.gitbook/assets/Simple Code Diagram 3.png" alt=""><figcaption></figcaption></figure>

## Quit OOP

Object-oriented programming is the most complicated and least readable way of coding. The problem is with the _abstraction_, _inheritance_, and _overriding_ mechanism. It goes against everything that simple coding is.

* It separates what belongs together and puts together what may not.
* It adds the strongest dependencies to the code.
* It enforces indirection and abstraction.
* Every class is an incomplete fragment despite its own _encapsulation_ principle.
* It does not decrease cyclomatic complexity.
* It is easy to misuse OOP.

Since we want to [separate the data and procedural classes](../oop/separate-data-and-procedures.md), we don't even have the _classes_ that OOP was invented for. It is simply not necessary.

We can replace OOP with _composition_ or _interfaces_.

Every object-oriented programming language is a _structured language_ too. It means that we can write _subroutines_ and call them. Use your OOP language as a structured language.

## Separate everything

We have to separate everything in the code in _'time and space'_.&#x20;

'In space' means that we should split the source code into _small_, _independent_, easy-to-understand, and easy-to-maintain parts. We should do this on all levels: methods, classes, packages, modules, etc.

We should create these small, independent parts by the following rules:

* Identifying business features, functions, steps, and use cases.
* Single responsibility principle.
* High cohesion.

'Separation in time' means that we should identify and design the steps of the algorithm that can be executed after each other. For this, we should break down the implemented functionality into use cases and the use cases into steps. In the code, we should [separate the implementation of the use cases](../simple-code/separate-use-cases.md).&#x20;

The output of one step will be an intermediate result that will be the input of the next step. It is especially important in _data-processing_ code. We should [separate data collection and preparation from the processing of the data](../simple-code/separate-data-collection-and-processing.md) so that both steps will be simpler and more independent.

We should strictly separate the implementation of different _business functions_ so that modifying one will not affect the others.

## Decrease branching

Branching is what we most simply do with the `if - else if` commands. It makes the program more complex and that is what we measure with _cyclomatic complexity_.

But the code checker tools measure it only in one method or class. If the program is full of branching then it has very high complexity. Programmers will not be able to keep every possible outcome in mind. Every change in the code will be risky and lead to bugs.&#x20;

Besides the obvious branching commands there are other hidden branchings we must be aware of:

* `if - else if` or `switch` commands
* ternary expressions
* nullable or `Optional` values (because we will have to check before usage`)`
* polymorphic classes

The possible ways to decrease the number of branchings are based on the above situations:

* Put related static constants in enums to reach them without branching.
* [Separate use cases and never join them again into a common code.](../simple-code/separate-use-cases.md)
* [Create data models without nullable or Optional members.](../simple-code/create-data-models.md)
* Avoid explicitly passing or returning `null`.
* Quit OOP

## Simple by default

We, programmers, like to write code. We like to create abstract, generic solutions so that we can _automate_ the tasks of the program. We are also prone to jump into coding as soon as possible, instead of spending more time with the specification or design. I think this is only a habit that we should not follow.

The problem is that these complex and [ad-hoc solutions](../oop/what-is-the-problem-with-inheritance.md) will require a very high maintenance time from the team. They also introduce a lot of dependencies between the features.

Our programming languages can also be misleading because they offer too many techniques and possibilities. For example, they are object-oriented. But that does not mean we should use OOP for every task _by default_. OOP is only a tool, and it is the most expensive one by the way.

The same goes for other language tools like generics or, lambdas. Not to mention the design patterns. Don't use them by default.

All modern programming languages are _structured languages_. That means that we can write sub-routines and call them directly. We can also organize them into components. We should stick to this approach by default, and choose complex solutions only when really needed.&#x20;

Before deciding to implement a complex solution we should properly _design_ it. We should discuss them with the team, and estimate their complexity and _maintenance cost_. If they are high then we should reject them.

Always do direct programming by default, instead of using _indirection_. Call-backs, frameworks, lambdas, etc. are only code fragments. They make it impossible to follow the business logic they implement.

## Focus on business logic

We, programmers, like to think in terms of coding. We like to write our solutions and structures in the code and then we groom them. I suggest always thinking in terms of the specification instead. Don't get lost in the implementation details.

We also like to jump into coding as fast as possible. I suggest instead, that we spend more time on the specification and design. We should break down the specification into _features_, _use cases_, _edge cases_, and _steps_. We should create examples, especially for complex data processing. Examples will also help later to find bugs or undetected edge cases.

If we cannot write down with clear text what the program does, if we cannot draw a flowchart, and if we cannot create an example for it, then we won't be able to implement it in any programming language.

In an ideal way, we should refine the specification into a pseudo-code. And then the real code should contain the pseudo-code. The program should implement the steps in the pseudo-code. What if we treated specification, design, implementation code, and even test code as one integrated document?

The steps or 'commands' of the pseudo-code will be the names of types, variables, and procedures. That's why names in the code are more important than the actual implementation. But only if we use business-relevant names that describe the business logic. Avoid using technical names, e.g. don't call an object 'object', don't call a map a 'map', etc.

Strive to separate business code and technical code. Technical implementation details should not pollute the business-relevant code and the other way around: business code should not be dispersed in a mass of technical code. Business logic should not be hidden as an implementation detail somewhere in the code.

Organize the code by business logic. Implement one feature in one place. Implement one use case in one place. Prefer this approach, instead of creating technical layers.

_"What does this code do?"_ That's what we usually ask when reading a code. I suggest continuously asking it also when writing the code. If we do not write the business logic into the code, we won't be able to read it!&#x20;
