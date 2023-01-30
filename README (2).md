---
description: 2023.01.30
---

# Simple Code Overview

{% hint style="danger" %}
Draft
{% endhint %}

## Separate everything

Separate in 'time and space'

* Time
  * Identify steps&#x20;
  * Create sequence of steps
* Space
  * Different features and use cases by different code
  * No common code

### [Separate data and procedures](oop/separate-data-and-procedures.md)

[Create data models](separate-data-collection-and-processing/create-data-models.md)

* For data processing
* Model the data
* Create data loader/collector
* Java: implements equals(), hashcode() and toString()
* Avoid using Maps in data models

Create code units with

* Well defined and immutable input data model
* Well defined and immutable output data model
* No additional data collection during data processing

Test code units simply

* Define input
* Define expected output
* Test equality

### Separate steps in time

[Separate data collection and data processing](separate-data-collection-and-processing/)

Always think about what can be distinct steps

### Separate features

Separate features

* Avoid common code above different features

[Separate use cases](separate-use-cases/)

* As early as possible
* In data models
* Never join separated use cases

### Separate method types

Orchestrator/dispatcher method

* One branching
* Redirecting method outputs to method inputs.

Implementation method

* Implements one thing.
* Usually returns a result.

### Separate constants

Don't collect constants on the top of the class

[Don't collect constants in a class or interface.](do-not-create-constant-collection-classes.md)

Put constants in the class that is responsible for it by business logic.

Collect constant value sets into `enum`s.

### Separate business code and technical code

Hide technical details behind business logic

Don't inline business functionality

Don't implement unnamed functionality

<details>

<summary></summary>

* Bad: `x.substr(2,5)`&#x20;
  * inlined in multiple places&#x20;
* Good: `getSomeCode(x)`&#x20;
  * implemented once
  * called from multiple places

</details>

### Organize code by SRP

[Single Responsibility Principle](single-responsibility-principle.md)

* Everything should do only one thing
* On every level of the code structure
  * method, class, package, module, etc.

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
