# Classes

### Two Types of Classes

#### Procedural

Business logic or Service

* Stateless, singleton or static if possible
* Instantiated mostly by the DI framework - _Spring, Java EE_
* If stateful, create it from the code with `new`

#### Data structure

Entity, DTO \(Data Transfer Object\)

* Only data members
* No business logic
* Always instantiated as new - _by the database layer or with new from the code_
* Accessors/mutators are questionable - _getters/setters_

### Rules

* One reason to exist, change
* "Small"
* No "God" class - _"Sack", "Blob"_
* Encapsulation \(hiding, protection\) decreases dependency - _Other classes cannot depend on this_
* Tight cohesion

### Cohesion

* Implements the "one thing" rule
* Contains only dependent members
* Refactor to cohesive classes
* There will be many small classes - _Like a toolbox with drawers_
* Reduces amount, cost and risk of changes

### Interfaces

* Create interfaces for service classes -_but not always paranoidly for everything_
* Prefer interfaces to parent classes
* Create marker interfaces

### Class Smells

#### No meaningful name

* You cannot give a meaningful name - _e.g. "Parent", "Common", "Processor", etc._

#### Unnecessary polymorphism

* Polymorphic class is not used as polymorphic - _never declared to parent type - see later_

#### Does more things - Low cohesion

* Many methods - _"God" or "Blob" class_
* Methods of a class can be split into distinct call chains - _they should be in separate classes_
* Test coverage is not visible or cheating
* Refactor to composition + Facade pattern

Example: Refactoring low cohesion

![](../../.gitbook/assets/refactoring-low-cohesion.png)

## 

