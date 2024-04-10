---
description: DRAFT
---

# Data Should Be Immutable

The next time you go to a job interview, please do the following experiment:

> Say "Hi, my name is John."
>
> A little later say "No, sorry, my name is Dave."

See whether you get the job.

## Problems with mutable data

### Unreliable data

Imagine the same experiment in the code:

#### Non-final variable:

```java
String firstName = "John";

// Code lines...

firstName = "Dave";

// Code lines...

```

Now, what is the name really? The code lines before the modification read the variable as "John", the lines after that read "Dave".

#### Mutable variable

The same happens with a final but _mutable_ variable:

```java
Name name = new Name("John", "Smith");

// Code lines...

name.setFirstName("Dave");

// Code lines...

```

Is he then "John Smith" or "Dave Smith"?

So it means the following problem:

{% hint style="warning" %}
Mutable data is unreliable. We never know whether they have a final value.
{% endhint %}

### More ifs — more branching

### Cannot follow the business process

#### Global variables

Every programmer knows that they should not use global variables. But they still use them, for example as permanent configuration data. The problem is the usage of _mutable_ global variables.

If any part of the code can modify the global variable at any time then we lose the _sequential nature_ of the program.

{% hint style="warning" %}
Mutable data make it hard to see the correct order of business events.
{% endhint %}

#### Instance variables

Instance variables of stateful classes cause the same problem. Even if the class is immutable for the clients, it is mutable for its own member methods. If any method can read and write the instance variables then we cannot see the steps of the business logic.

Unfortunately, this is a fundamental problem with object-oriented programming. It goes against the clean code principles. That is another reason why I suggest to [quit OOP](../oop/do-not-use-inheritance.md).

### Separate business steps

The solution is, as I suggested in another article:

{% hint style="success" %}
Separate steps of the business process. [Separate data collection and processing](separate-data-collection-and-processing.md).
{% endhint %}

The _immutability_ of the data plays an essential role in this. One piece of data is created only in a well-defined step of the business logic. It is not modified later. That's how we know that this distinct step of the business process is done. When looking at the next code we don't have to take care of the already finished steps.

As always: focus on the business logic. Break down the business logic into steps and implement these steps.

## Make data immutable

### Technically immutable

Making it really immutable is not easy. It may not be enough that the data type has no mutators (setters). If it is a composite of other structured data then:

* all contained data must be immutable
* or if not, then constructors should make a deep copy of the data
* accessors (getters) should also make a deep copy of the returned data,
* or wrap them in immutable types if possible (e.g. immutable collections)

### Use records

exactly for this purpose

### Effectively immutable

Collectors or factories. BL is more important

## Other issues with mutability

### Mutable data

Sometimes data can or must be mutable if this is its purpose. For example error collectors or loggers.

In this case we should limit the mutability to the only necessary interface, and we should prevent the arbitrary modification.

For example, if we collect errors then the data should have an add method only. But we should prevent the error collection from overwriting or deleting. We can do this with the usual solution: getters should wrap the collection in an unmodifiable collection before returning.

We should also make sure that the elements in the collections are immutable too.

```java
// Allowed
errors.addError(...); 
errors.getErrors(); // Immutable return

// Not allowed
errors.setErrors(...);
errors.getErrors().set(...); 
errors.getErrors().get(...).setErrorMessage(...);
```

### Initialization vs. default values

I saw a question on StackOverflow, about how we should correctly initialize a variable.

Also, programming languages such as Java initialize variables with null if they are declared but no value is given to them.

The real answer is: treat data as immutable.

Why would you create a variable without a value?&#x20;

### Return value

That's why it is a bad habit to create return values like this:

```java
Object calculateName() {
    String name = "N/A";
    if(...) {
        name = "John";
    } else if (...) {
        if(...) {
            name = "Dave";
        }
        // Code lines...
        if(...) {
            name = "Anna";
        }
    }
    return name;
}
```
