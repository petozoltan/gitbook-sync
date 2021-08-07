# Special Cases

### Warnings

* Do not ignore compiler/IDE warnings
* Each warning is a potential/existing bug
* Do not suppress warnings - _Find the correct solution instead_
* Use the capabilities of your IDE - _Turn on most of the possible warnings_
* Do not add new code with warnings!
* Use code checkers - _CheckStyle, FindBugs, PMD, Sonar, etc._

Example: Bad: Suppressed warnings

```java
// Many tricks for one unused parameter

// CHECKSTYLE:OFF
@SuppressWarnings("unused")
private void addDescription(Type type, Contract contract, String comment) { // NOSONAR
    contract.setDescription(createDescription(contract.getType(), comment));
}
// CHECKSTYLE:ON
```

Example: Good: Fixed problems

```java
private void addDescription(Contract contract, String comment) {
    contract.setDescription(createDescription(contract.getType(), comment));
}
```

### Logging

* Use correct logging levels
* Log stack trace only for unexpected program errors
* Create \(concatenate\) expensive message only if logged - _see SLF4J capabilities_

### Java

* Never use raw types - _always use generics correctly_
* Avoid using reflection
* Know you API - _use utility methods_



