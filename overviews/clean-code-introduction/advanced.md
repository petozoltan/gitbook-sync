# Advanced

### What clean code is not, and what it is instead

Not code beautifying

* Code correctness

Not a set of mechanic rules

* Continuous thinking
* Half science, half art
  * continuous shaping the code
* Principles instead of rules
* Terms
* Violations are only 'code smells'

No numeric rules

* Only one numeric rule: it does 1 thing.
* 'Simple' instead of 'small'.

No boilerplate code templates

* Alway the best simplest direct solution

Not for code checkers

* Human readability, expressivity 

Not matter of taste

* Quest for an optimal implementation

Not waste of time

* Aims to finish the code
* Refactoring is not evil
* Technical debt is evil

Not easy

* Self discipline
  * it is easy to know the rules but not easy to apply them to ourselves 
  * easy to see other's bad code but not easy to recognize when we do them
* Long practice

### The ultimate goals of clean code

The software product should be...

* Error free
* Finished
* Maintainable

We realize the goals through...

* Expressiveness
* Granularity

### When is the code good?

If it is _decidable_ whether it is good.

* It is a comparison
  * Specification vs. implementation
  * Declaration vs. definition
  * Names vs. code blocks {}

### Single Responsibility Principle

[SRP is the core rule of clean code.](../../single-responsibility-principle.md)

### Reading the code with clean code view

I see independent, named code blocks { }:

* Does every code block {} do what its name tells?
  * Class's/Method's full declaration vs. definition block {}
* For one code block, I do not care about anything else outside
  * Callers of the methods
  * Methods called from this code block
* For parent classes, I don't care about the children
  * OCP, SRP, spaghetti
* Does everything have a name?
  * Methods: No inline implementation
  * Classes: No low cohesive classes

### Modifying the code with clean code view

Before modification

* Understand affected parts
* Check cleanness 
* If not clean, refactor

Do modification

* Change names first
* Implement code



