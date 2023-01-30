# Clean Code Approaches

### Simple Design / Emergent design

Author: _Kent Beck_

* Runs all the tests
* Contains no duplication
* Expresses the intent of the programmer
* Minimizes the number of classes and methods

> Perfection is achieved, not when there is nothing left to add, but when there is nothing left to remove. \(Antoine de Saint-Exupery\)

### Pseudo code

* The code should look like a pseudo code
* The types and methods and names we create are pseudo code really
* DSL - Domain Specific Language
* The business analyst should be able to understand it

Example: Pseudo code

```text
"Take the higher prices":

if Master prices are higher than in Increase then
   apply Master prices to the Increase
and
   apply Master conditions to the Increase
if Master discount fare is higher than in Increase then
   apply Master discount fare to the Increase
```

Example: Good: Java code

```java
void compareAndUpdateIncrease(PricingResponseDTO masterResponse, PricingResponsePaxfares masterPaxFares, 
        PricingResponseDTO increaseResponse, PricingResponsePaxfares increasePaxFares) {

    if (isMasterPriceHigherOrEqual(masterPaxFares, increasePaxFares)) {
        updateIncreasePrices(masterPaxFares, increasePaxFares);
        updateIncreaseConditions(masterResponse, increaseResponse);
    }

    if (isMasterMaxDiscountFareHigher(masterPaxFares, increasePaxFares)) {
        updateIncreaseMaxDiscountFares(masterPaxFares, increasePaxFares);
    }
}
```

Example: Change request

```text
"Always take the conditions from the master."
```

Example: Good: Changed code

```java
void compareAndUpdateIncrease(PricingResponseDTO masterResponse, PricingResponsePaxfares masterPaxFares, 
        PricingResponseDTO increaseResponse, PricingResponsePaxfares increasePaxFares) {

    if (isMasterPriceHigherOrEqual(masterPaxFares, increasePaxFares)) {
        updateIncreasePrices(masterPaxFares, increasePaxFares);
    }

    updateIncreaseConditions(masterResponse, increaseResponse);

    if (isMasterMaxDiscountFareHigher(masterPaxFares, increasePaxFares)) {
        updateIncreaseMaxDiscountFares(masterPaxFares, increasePaxFares);
    }
}
```

### Specification vs. Implementation

* Specification: Name or description or "contract" or "promise" = _class and method declarations_
* Implementation: "internal part" that fulfills the promise = _code block {}, package content, etc._
* Every code unit is a "separate world" - _e.g. class or method blocks_

### What does this code do?

* The reader will ask it
* The developer should ask it

### Metric Rules

* There are NO numeric rules like maximum lines of code, number of parameters, level of indentation, etc.
* The only numeric rule is: One code does one thing + One thing is implemented once
* Classes and methods should be "small" but it is not exactly defined

### Developers

* Do not only satisfy the compiler or the unit tests
* Be the reader of your own code - _stop and think_
* "Tell the story" with proper types and names
* Describe the business logic with English words as much as possible

### Avoid "Enemies" of the Code

* No duplication - _DRY_
* No inline implementation
* No misplaced code
* No parallel development - _"spaghetti code"_
* No unused code - _"dead code"_

### Clean Code is an Art

* Not a set of mechanical rules
* More principles to apply
* Continuous thinking and shaping the code - _"step back"_

### Scrum

* "Code is clean"' should be part of Definition of Done



