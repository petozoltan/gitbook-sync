---
description: DRAFT
---

# Data Should Be Immutable

## Experiment

The next time you go to a job interview, please do the following experiment:

> Say "Hi, my name is John."
>
> A little later say "No, sorry, my name is Dave."

See whether you get the job.

## Example

Imagine the same experiment in the code:

#### Non-final variable

```java
String firstName = "John";

// Code lines...

firstName = "Dave";

// Code lines...

```

Now, what is the name really? The code lines before the modification read the variable as "John", the lines after that read "Dave".

#### Mutable object

The same happens when we don't overwrite the variable but modify it:

```java
Name name = new Name("John", "Smith");

// Code lines...

name.setFirstName("Dave");

// Code lines...

```

Is he then "John Smith" or "Dave Smith"?

## Arbitrary changes

The problem is not that the data is technically mutable. The question is, where and how we modify the data?

Drawing: Data collector -> Data processor

Data collector can write the data by constructors or mutators (setters). That is not the problem.

The problem is when the Data processor modifies the data.

Why? The answer is, as usual:

Always focus on the business logic. Break down the business logic into steps and implement them. If one step is to collect the data but after that we modify the data, then the collect step is simply not finished. It is not implemented correctly. We have a spaghetti code then.

Create data as true immutable or treat it as immutable

Use records, which are immutable.

## Technically of effectively immutable

## Use records

## Global Variables

Ever programmer knows that we should not use global variables.

But we still use them, for example as configuration data or current user.

The problem is the usage of mutable global variables.

Then the value of the variable may change in many places and we lost the sequential nature of the program, i.e. steps of the business logic after each other.

## Mutable data

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

## Initialization vs. default values

I saw a question on StackOverflow, how we should correctly initialize a variable.

Also programming languages as Java initialize variables with null if they are declared but no value is given to them.

The real answer is: treat data as immutable.

## Return value

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
