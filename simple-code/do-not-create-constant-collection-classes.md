---
description: 2016.07.31
---

# Do Not Create Constant Collection Classes

Programmers often create separate classes to store constants of a certain area, "to have them at one place" or "to avoid polluting" the procedural classes. But it is not enough to make the code clean. What is the problem with them and how can we solve it?

### Interpretation problems

When new constants have to be created it is not mandatory to add them to the collection class. Developers can decide to add constants to the collection or to create them somewhere else. Unfortunately, this is another problem that makes OOP very hard:

> If it is not obvious where to write the new code then the chaos begins.

### Classes should not always be modified

It breaches the [Single Responsibility Principle](../explained/single-responsibility-principle.md) because such classes may contain information for more different functionality.

### Finish and test

At a certain point, a class must be tested and finished, in order to have a reliable code. But constant collections are loose and generic, so they are practically never finished. When you look at such a class, you cannot decide whether it is finished or not.

### Prefer enums to constants

In most cases, it is better to use enums instead of constants. Enums have more benefits over constants:

* Enums define and limit a specific _value set_. So it is clear to which enum a new value has to be added.
* They are type-safe. Elements of different value sets are not assignable.
* They can be provided with additional useful information. I call it _mapping_ all information that belongs together in one enum constant.

### Split into more enums

Usually, a constant collection should be split into more than one enum. You can see a clear sign for that in the following cases:

* The constants have different types.
* The constants' names begin with different _prefixes_.
* Constants are grouped by comments.

### Example

With a very simple example, this class is simply a collection of constants:

```java
public class UserConstants {

    // Gender
    public final static int CODE_MALE = 1;
    public final static int CODE_FEMALE = 2;

    public final static String LABEL_MALE = "Male";
    public final static String LABEL_FEMALE = "Female";

    public final static String TITLE_MR = "Mr.";
    public final static String TITLE_MS = "Ms.";
    public final static String TITLE_MRS = "Mrs.";

    // Messages
    public final static String TITLE_NAME_MISSING = "Missing name";
    public final static String MSG_NAME_MISSING = "Please enter your name";
    public final static String TITLE_PHONE_MISSING = "Missing phone number";
    public final static String MSG_PHONE_MISSING = "Please enter your phone number";

    // etc.
}
```

But it should be refactored to different enums:

```java
enum Gender {

    MALE(1, "Male"),
    FEMALE(2, "Female");

    private int code;
    private String label;

    private Gender(int code, String label) {
        this.code = code;
        this.label = label;
    }

    public int getCode() {
        return code;
    }

    public String getLabel() {
        return label;
    }
}

enum Title {

    MR("Mr."),
    MS("Ms."),
    MRS("Mrs.");

    private String label;

    private Title(String label) {
        this.label = label;
    }

    public String getLabel() {
        return label;
    }
}

// etc.
```

At first glance, it seems that the class with the constants is simpler and shorter than the enum classes.

But imagine that it contains hundreds of constants and their number is always growing, while the enums will rarely grow. Actually, the pure informational lines in the enums are only these ones, which are already shorter and more descriptive than the original:

```java
enum Gender {

    MALE(1, "Male"),
    FEMALE(2, "Female");

    ...
}

enum Title {

    MR("Mr."),
    MS("Ms."),
    MRS("Mrs.");

    ...
}
```

On the other hand, related constants are not declared to be related so you have to pollute your business code with such lines, for example:

```java
    switch (code) {
    case CODE_MALE:
        doSomething(LABEL_MALE);
    case CODE_FEMALE:
        doSomething(LABEL_FEMALE);
    default:
        throw new IllegalArgumentException();
    }
```

Unfortunately, developers tend to write this code in more places in different forms, which means that this business information is implemented more times. It is _code duplication_. But even if they implement it only once, it is more descriptive in the enum. We should just add some "boilerplate" methods to our enum, which do not repeat the information:

```java
enum Gender {

    MALE(1, "Male"),
    FEMALE(2, "Female");

    ...

    public static String getLabel(int code) {
        return getByCode(code).getLabel();
    }

    public static Gender getByCode(int code) {
        for (Gender gender : values()) {
            if (gender.getCode() == code) {
                return gender;
            }
        }
        throw new IllegalArgumentException();
    }
}
```

### Do not mix constants with procedures

When a set of public constants are written in a class that also contains public procedures, it will lead to the situation, that the class frequently changes only because of the constants.

### Avoid other types of collection classes

Of course, constants are only one example. But developers also create classes that hold a collection of independent or loosely coupled _methods_. The most common example is a _service_.

A service must provide a public interface, i.e. a set of public methods. To avoid creating a method collection class we should apply the _Facade_ design pattern. So the service class should be "thin" by providing the methods and delegate them to specific, highly cohesive classes.

Note: Check out the API documentation of Spring's [@Service](http://docs.spring.io/autorepo/docs/spring-framework/3.0.x/javadoc-api/org/springframework/stereotype/Service.html) annotation:

> Indicates that an annotated class is a "Service" (e.g. a business service facade).

### Do Not Collect Constants at the Top of the Class

Despite that the "magic values" have been transformed into named constants, it may be the incorrect place to define them in the same class.

{% tabs %}
{% tab title="Magic number" %}
```java
class ContractService {
    
    void doSomethingSpecial() {
        updateContractLog(getUser("U1234")); // Special user's code
    }
}
```
{% endtab %}

{% tab title="Constant" %}
```java
class ContractService {

    String SPECIAL_USER_ID = "U1234";
    
    void doSomethingSpecial() {
        updateContractLog(getUser(SPECIAL_USER_ID ));
    }
}
```
{% endtab %}

{% tab title="Correct" %}
```java
package user;

enum UserConstants {

    SPECIAL_USER_ID("U1234");
    
    ...
}

package contract;

class ContractService {

    String SPECIAL_USER_ID = "U1234";
    
    void doSomethingSpecial() {
        updateContractLog(getUser(UserConstants.SPECIAL_USER_ID));
    }
}
```
{% endtab %}
{% endtabs %}

In the upper example, the `ContractService` class is not responsible for defining the constant for the special user ID. It is rather related to User services.
