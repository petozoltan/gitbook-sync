---
description: 2023.01.30 DRAFT
---

# Clear Code Rules

## [Separate everything](clear-code-overview.md#separate-everything)

<details>

<summary>Separate steps</summary>

* Split the algorithms into separate steps that can be done one by one.
* Design the intermediate data to be created by the steps and used by the next ones.
* Create sequences of steps. That is the easiest to be understood by the human mind.
* [Separate data collection and data processing](../simple-code/separate-data-collection-and-processing.md).

</details>

<details>

<summary>Separate features</summary>

Separate features

* Implement different features and use cases in different parts of the code.
* Avoid common code above different features.
* Avoid implementing use cases with a common code and then branching them from there.

[Separate use cases](../simple-code/separate-use-cases.md)

* As early as possible.
* [Already in data models.](../examples/separate-use-cases-with-data-model.md)
* Never join use cases again, once they are separated.

</details>

<details>

<summary>Separate data and procedures</summary>

[Separate data and procedures](../oop/separate-data-and-procedures.md)

[Create data models](../simple-code/create-data-models.md)

* For data processing always design the data first.
* _Model_ the business results with the data. That's why it is called a 'data model'.
* Create separate data loaders/collectors and data processors.&#x20;
* In Java implement `equals()`, `hashcode()` and `toString()`  of data classes.&#x20;
  * It will help the testing and debugging.
* Avoid using Maps in data models. They will make the data 'unfinished'.

Create code units with

* a well-defined and immutable (or effectively immutable) _input_ data model,
* and a well-defined and immutable (or effectively immutable) _output_ data model.
* Avoid additional data collection during data processing.

Test code units with input/output data.

* Create input data.
* Create expected output.
* Simply test their equality.

</details>

<details>

<summary>Separate method types</summary>

Dispatcher method

* One branching
* Redirecting method outputs to method inputs.

Implementation method

* Implements one thing.
* Usually returns a result.

Strive to create only these two method types.

* Break long methods into multiple methods until you reach it.

</details>

<details>

<summary>Separate constants</summary>

Don't collect constants at the top of the class.

[Don't collect constants in a class or interface.](../various/do-not-create-constant-collection-classes.md)

Put constants in the class that is responsible for it by business logic.

Collect constant value sets into `enum`s.

</details>

<details>

<summary>Separate business code and technical code</summary>

Hide technical details behind business logic.

Don't _pollute_ business functionality with technical details or the other way around.

Don't mix technical implementations with business logic implementations.

* Don't extend generic technical classes (e.g., Collections) to create a business-specific implementation.

Always name variables after their business meaning.

* Avoid technical names.
* E.g., don't call a map 'map' a result 'result' etc.

</details>

<details>

<summary>Organize code by SRP</summary>

[Single Responsibility Principle](../various/single-responsibility-principle.md)

* Every part of the code should implement only one part of the business logic. (The original SRP.)
* Every part of the business logic should be implemented by one part of the code.
* A 'part' of the code can be any level, like a method, class, package, module, etc.

Apply high cohesion

* Put together what belongs together.
  * Methods or classes that call each other.
* Method and class implementation are simply code blocks that hold elements together.
* Create inner classes to group a few methods within a larger class.
* A package is also a bracket that holds classes together
* Minimize the interface to a group of procedural codes.
  * One public method for one class.
  * One public class for one package.

Treat classes as code units

* closed
* finished
* final
* tested

</details>

## [Simplest solution by default](clear-code-overview.md#simple-by-default)

Consider maintenance costs when choosing a solutions.

Directly call subroutines

No internal ad hoc frameworks

No pets - they will become monsters

No fancy solutions

No tricky solutions

<details>

<summary>Quit OOP</summary>

Don't use inheritance. Overriding is forbidden.

Use composition.

Use classes to simply organize code into components.

Use your programming language as a structured language.

* Write procedures and call them directly.

</details>

No frameworks over frameworks

Use them as it is

Avoid design patterns

No Builder

No visitor

Use complex solutions only if really necessary

Design and document them.

## Avoid indirection

Preference

No indirection

Interface

Lambda

Subclass

Avoid passing lambdas to methods

Minimize to 'attributes'

Avoid call-back classes

Avoid child classes

Don't pass Maps as parameters

Use them where you create them

Don't use Maps in data models

Minimize callbacks

Callbacks are code injection

Callbacks are branching

Callbacks are parallels

Callbacks are "frameworks"

Image with callback: parallels

## [Decrease branching](clear-code-overview.md#decrease-branching)

Separate use cases

As early as possible

In data models

Never join separated use cases

Organize ifs properly

Use guardian pattern

Decrease indentation

Don't indent the main payload of the method

Consider the cyclomatic complexity of an entire implementation of a feature or use case, not only of one method.

Create sequences

Image with sequences

Image with callback

Image with common code

Image with branching

Branchings are parallels

Write common code that is really common

Put related static information into enums.&#x20;

* Once you have the enums, you can get the related information without branching.
* Don't use it to reach procedural code. I.e. don't use it for functions, lambdas, method references. They need a different solution.
* In one case you can use method references: for data attributes. ([Because they are actually not procedures.](../oop/separate-data-and-procedures.md#the-new-classes))

## Decrease dependencies

Make everything final / immutable

or effectively final / immutable

Data should be final / immutable

Avoid side effect programming

Mutables cannot be used as keys.

Classes should be final

But because of the mocking framework they cannot be

Investigate #xx

Organize code by SRP

Treat classes as code units

closed

finished / final

tested

minimize interfaces

Access the one functionality through one way (one method)

high cohesion

low coupling

everything should do only one thing

method

class

package

module

Don't increase visibility

Minimize interfaces

* Access the one functionality through one way (one method)
* low coupling

## [Focus on business logic](clear-code-overview.md#focus-on-business-logic)

<details>

<summary>Fully understand the business requirement before coding</summary>

Don't start with the coding.

* Put aside your programming language.
* Put aside your implementation ideas.
* Don't code until you don't understand the specification perfectly.

Don't skip the design.

* Create examples if necessary.
* Create graphs or UML-s if necessary.
* Identify use cases.

</details>

<details>

<summary>Refine the specification into code</summary>

Refine the specification into a pseudo-code.

* This is a language-independent implementation of the business logic.
* This is the actual program programmers should write!

Implement the pseudo-code in your programming language.

* Names in the program should be the same as in the pseudo-code.
* Implement the steps of the pseudo-code in the real code.
* E.g., the call hierarchy of the methods should be the pseudo-code.

Chose the most simple and straightforward implementation.

* Usually, this consists only of simple method calls.
* The methods are simply grouped into components (procedural classes).

</details>

<details>

<summary>Organize code by business logic</summary>

Implement one feature under one package or module.

Name components and variables by their business meaning.

* Name them by actions, functions, use cases, etc.
* Avoid technical names.
* Reading the names in the code should show the business logic.
* Names are important.

</details>

<details>

<summary>Always provide business code with names</summary>

Extract implementations of the business logic into methods and components with proper names.

Don't inline business implementation into other code.

Implement one business functionality only once.

Avoid code repetition.

</details>

<details>

<summary>Separate business code and technical code</summary>

See above, under [#separate-everything](clear-code-rules.md#separate-everything "mention").

</details>
