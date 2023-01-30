# Object Oriented Programming

### OOP Paradigm

The original paradigm just to remember:

* Encapsulation
* Inheritance
* Polymorphism

### Clean OOP Principles

* Tight cohesion
* Loose coupling
* Responsibility - _where to write code?_

### Separation of concerns

* Creation - _Dependency Injection_
* Configuration
* Services, components - _Business logic_
* Data - _Entities, DTOs_
* Layers
* Logging - _Framework or AOP_

### Dependency Injection

#### Dependency Inversion

* The paradigm
* A.k.a. Inversion of Control, IoC
* Always depend from the abstraction
* The more abstract, the more robust

Example: What is inverted in DI?

![](../../.gitbook/assets/uml-dependency-inversion.png)

#### Dependency Injection

* Implementation of the Dependency Inversion
* Mostly done by a DI framework -Spring, Java EE, ...
* Easy to test -using mocks, test doubles

Example: Bad: Without dependency injection

```java
public class FileHistoryService {

    // Factory - Hard to replace implementation, hard to test
    private IFileHistoryDao fileHistoryDao = DaoFactory.getFileHistory();

    // Instantiation - Depends on implementation, may be more complex
    private FileHistoryToFileHistoryDtoAssembler fileHistoryAssembler = new FileHistoryToFileHistoryDtoAssembler();

    // Static methods - Depends on implementation, not polymorphic
    private FileHistory createFileHistory() {
        HttpHistoryAuthorHelperTAFile.fillAuthorFromHttpRequest(fileHistory);
    }
}
```

Example: Good: Dependency injection by a DI framework

```java
@Component
public class FileHistoryService {

    @Autowired
    private IFileHistoryDao fileHistoryDao;
    @Autowired
    private FileHistoryToFileHistoryDtoAssembler fileHistoryAssembler;
    @Autowired
    private HttpHistoryAuthorHelperTAFile authorHelper;
}
```

### Inheritance over instanceof

Do not use instanceof and isAssignableFrom\(\)

* it adds dependency
* it adds duplication
* refactor to polymorphism or patterns

### Composition over inheritance

#### Problems with inheritance

* Too strict
* Hard to develop - _one child changes a certain way the other one does not_
* Do not use inheritance only for a "common" code
* Parent and children are be changed together - _spaghetti code_
* Favor composition to inheritance - _Item 16 in Effective Java \(2nd Edition, Joshua Bloch, 2008\)_
* Overridden methods are unreadable and fragile - _Item 17 in Effective Java \(2nd Edition, Joshua Bloch, 2008\)_

#### Code Smells

* Parent must be changed when children change, abstract methods should be added
* The parent's name is "Common..." - _a class should have an intentional business name_

#### Use inheritance only for

* Real polymorphism
* Polymorphic usage - _declared as a "parent" type_
* Design patterns

### Law of Demeter

* "Only talk to immediate friends"
* Do not depend on the implementation details other classes
* Use only one level of abstraction
* "Wallet" rule
* "Count of dots" rule - _But not simply a dot counting law_
* It depends on that the used class is procedural or a data structure \(see Classes\)

Example: Bad:

```java
// Depends on implementation of neighbors of neighbors...
String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();

// More levels of abstraction, reaches through layers
public boolean checkPassword(String name, String pwd) {
    userService.checkPassword(pwd); // It already uses UserDao
    User user = userDao.findUser(name); // It should not
}
```

### S.O.L.I.D.

Not in the book but also Uncle Bob.

#### Single Responsibility

* A class should have only one reason to change
* Only a change in the specification should affect the implementation of the class

#### Open/Closed

* Software entities should be open for extension, but closed for modification

It can be more general:

* Software entities should NOT be open for extension
* Any class should be closed for modification - _not only parent classes_

#### Liskov Substitution

* Objects should be replaceable with instances of their subtypes without altering the correctness of that program.
* See also design by contract

#### Interface Segregation

* Many client-specific interfaces are better than one general-purpose interface.

#### Dependency Inversion

* Depend on Abstractions. Do not depend on concretions.
* Dependency injection is one method of following this principle.



