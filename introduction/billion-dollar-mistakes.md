---
description: DRAFT
---

# Billion Dollar Mistakes

<figure><img src="../.gitbook/assets/Billion Dollar Mistakes 2.png" alt=""><figcaption></figcaption></figure>

In this summary, I try to strip down the problems in programming to a few big mistakes. These problems make the code unreadable and unmaintainable and make software development very time-consuming.

_I took the click-bait title from this speech:_ [_Null References: The Billion Dollar Mistake_](https://www.infoq.com/presentations/Null-References-The-Billion-Dollar-Mistake-Tony-Hoare/)_._

## Object-oriented programming

#### Problems

OOP is a very hard-to-read and hard-to-write way of coding. It hides the business logic, which is the opposite of what the code should do.

It is the most expensive way of coding. Most of the coding time is spent solely on understanding and maintaining class hierarchies. This time is missing from working on the business requirements. So a lot of time is _wasted_.

Using OOP is not necessary. (At least in most of the programming situations.) So the price/benefit ratio is extremely high.

After separating data and procedures we don't have _classes._ As a consequence most of the OOP rules we know become invalid.

#### Solutions

* [Quit OOP](../oop/do-not-use-inheritance.md).
* [Separate data and procedures](../oop/separate-data-and-procedures.md).
* Use the Composite pattern.
* Model the real-life domain entities with the _data model_ and not with the procedural components.

## High number of branching

#### Problems

Branchings increase the cyclomatic complexity of the program. It is measured only for single methods but not for the entire program. We have a blind spot for this problem.&#x20;

We write ifs and other forms of branching everywhere in the code. We create class hierarchies and other patterns that are based on branching. We do it in an irresponsible way; we don't care how many branching we create.

The high number of branching is also a consequence of antipatterns, like passing and returning nulls or controlling the program flow with nulls. _(Spaghetti code,_ [_Insider trading_](../simple-code/separate-use-cases.md#insider-trading)_.)_

#### Solutions

* [Separate use cases](../simple-code/separate-use-cases.md). Separate use cases only once and as early as possible.

## Automation

#### Problems

We write code that automates the program in runtime.

Frameworks, common code.

This is not the program we should write.

Everything that is known in coding time should be written in the code and explicitly called from use cases.

#### Solutions

* .

## Incorrect Data Processing

#### Problems

We never identify a program as a "data processing code".

We should write components with clearly defined input and output data structures.

A "backend" is a data processing code.

#### Solutions

* .
