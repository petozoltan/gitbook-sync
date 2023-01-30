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

### [Separate Data And Procedures](oop/separate-data-and-procedures.md)

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

Separate features

[Separate use cases](separate-use-cases/)

* As early as possible
* In data models
* Never join separated use cases

### Separate business code and technical code

* Hide technical details behind business logic
  * E.g. no x.substr(2,5) in arbitrary places but getSomeCode(x)

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

Organize code by business logic

Feature

Use case

Separate business code and technical code

Consider maintenance costs when choosing a solution

Separate method types

Orchestrator/dispatcher

Implementation

## Simplest solution by default

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

## Focus on business logic

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
