---
description: 2023.02.12
---

# Simple Code Overview

<figure><img src="../.gitbook/assets/Simple Code Diagram 3.png" alt=""><figcaption></figcaption></figure>

## Quit OOP

Object-oriented programming is the most complicated and least readable way of coding. The problem is with the _abstraction_, _inheritance_, and _overriding_ mechanism. It goes against everything what simple coding is.

* It separates what belongs together and puts together what may not.
* It adds the strongest dependencies to the code.
* It enforces indirection and abstraction.
* Every class is an incomplete fragment despite its own _encapsulation_ principle.
* It does not decreasee cyclomatic complexity.
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

'Separation in time' means that we should identify and design the steps of the algorithm that can be executed after each other. For this, we should break down the implemented functionality into use cases and the use cases into steps. In the code, we should [separate the implementation of the use cases](../simple-code/separate-use-cases/).&#x20;

The output of one step will be an intermediate result that will be the input of the next step. It is especially important in _data-processing_ code. We should [separate data collection and preparation from the processing of the data](../simple-code/separate-data-collection-and-processing/) so that both steps will be simpler and more independent.

We should strictly separate the implementation of different _business functions_ so that modifying one will not affect the others.

## Decrease branching

Branching is what we most simply do with the `if - else if` commands. It makes the program more complex and that is what we measure with _cyclomatic complexity_.

But the code checker tools measure it only in one method or class. If the program is full of branching then it has very high complexity. Programmers will not be able to keep every possible outcome in mind. Every change in the code will be risky and lead to bugs.&#x20;

Besides the obvious branching commands there are other hidden branchings we must be aware of:

* `if - else if` commands
* `switch` commands
* ternary expressions
* nullable values (because we will have to check them for `null)`
* `Optional` values (similar to nullable values)
* polymorphic classes

The possible ways to decrease the number of branchings are based on the above situations:

* Put related static constants in enums to reach them without branching.
* [Separate use cases and never join them again into a common code.](../simple-code/separate-use-cases/)
* [Create data models without nullable or Optional members.](../simple-code/separate-data-collection-and-processing/create-data-models.md)
* Avoid explicitly passing or returning `null`.
* Quit OOP
