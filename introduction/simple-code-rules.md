---
description: 2023.01.30
---

# Simple Code Rules

{% hint style="danger" %}
Draft
{% endhint %}

## Separate everything

Separate the program in 'time and space'.

* Time
  * [Separate steps](simple-code-rules.md#separate-steps)
* Space
  * Implement different parts of the business logic in different parts of the code.

### Separate steps

<details>

<summary></summary>

* Split the algorithms into separate steps that can be done one by one.
* Design the intermediate data to be created by the steps and used by the next ones.
* Create sequences of steps. That is the easiest to be understood by the human mind.
* [Separate data collection and data processing](../simple-code/separate-data-collection-and-processing.md).

</details>

* Split the algorithms into separate steps that can be done one by one.
* Design the intermediate data to be created by the steps and used by the next ones.
* Create sequences of steps. That is the easiest to be understood by the human mind.&#x20;
* [Separate data collection and data processing](../simple-code/separate-data-collection-and-processing.md).

### Separate features

<details>

<summary></summary>

Separate features

* Implement different features and use cases in different parts of the code.
* Avoid common code above different features.
* Avoid implementing use cases with a common code and then branching them from there.

[Separate use cases](../simple-code/separate-use-cases.md)

* As early as possible.
* [Already in data models.](../examples/separate-use-cases-with-data-model.md)
* Never join use cases again, once they are separated.

</details>

Separate features

* Implement different features and use cases in different parts of the code.
* Avoid common code above different features.
* Avoid implementing use cases with a common code and then branching them from there.

[Separate use cases](../simple-code/separate-use-cases.md)

* As early as possible.
* [Already in data models.](../examples/separate-use-cases-with-data-model.md)
* Never join use cases again, once they are separated.

### [Separate data and procedures](../oop/separate-data-and-procedures.md)

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
* Simply test equality.

### Separate method types

Dispatcher method

* One branching
* Redirecting method outputs to method inputs.

Implementation method

* Implements one thing.
* Usually returns a result.

Strive to create only these two method types.

* Break methods into multiple methods until you reach it.

### Separate constants

Don't collect constants at the top of the class.

[Don't collect constants in a class or interface.](../simple-code/do-not-create-constant-collection-classes.md)

Put constants in the class that is responsible for it by business logic.

Collect constant value sets into `enum`s.

### Separate business code and technical code

Hide technical details behind business logic.

Don't 'pollute' business functionality with technical details or the other way around.

Don't extend generic technical classes (e.g. Collections) to create a business-specific implementation.

Always name variables after their business meaning.

* E.g. don't call a map 'map', a result 'result', etc.

Don't inline business functionality.

* Don't implement unnamed functionality.
* It would also lead to code repetition.

### Organize code by SRP

[Single Responsibility Principle](../explained/single-responsibility-principle.md)

* Every part of the code should implement only one part of the business logic. (The original SRP.)
* Every part of the business logic should be implemented by one part of the code.
* A 'part' of the code can be any level, like a method, class, package, module, etc.

Use high cohesion

* Put together what belongs together.
  * Methods or classes that call each other.
* Method and class implementation is actually a code block `{  }`&#x20;
* A code block is actually only a bracket that holds elements together.
* Create inner classes to group a few methods.
* A package is also a bracket that hold classes together
* Minimize interface to a group of code

Treat classes as code units

* closed
* finished / final
* tested

## Simplest solution by default

### Organize code by business logic

Consider maintenance costs when choosing a solution

Use language as a structured language

Directly call subroutines

No internal ad hoc frameworks

No pets - they will become monsters

No fancy solutions

No tricky solutions

Quit oop

No Inheritance

Override forbidden

See effective java

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

## Decrease branching

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

## Focus on business logic

Forget about coding

* Put aside you programming language
* Put aside your implementation ideas

Organize code by business logic

* Feature
* Use case

Refine spec and design before coding

* Refine to pseudo code
* Create names
* Implement the final steps
* Treat specification, design, implementation code, and test code as one integrated document

Identify use cases

Create examples

Separate business code and technical code

Extract named functionality

* Don't inline&#x20;
  * without name
  * at multiple places
