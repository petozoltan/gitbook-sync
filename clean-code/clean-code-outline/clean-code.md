# Clean Code

### Expectations

* The code should show what is does
* The code should show the intentions of its programmer - _Express what you will_
* The code should reflect the specification - _Business analysts should be able to see the business algorithms in the code_
* Reviewers should be able to decide whether the code is good or not
* Logical
* Direct, straightforward
* Reduce cost and risk of changes
* Good, correct
* Less bugs
* Code quality

> The main goal is to see that the code correctly does what the specification requires

### Goals

* Readable - _We spend much more time with reading than with writing._
* Understandable
* Simple
* Effective
* Easy to change - _Not "fragile"_
* Testable
* Fragmented
* Reliable
* Intentional
* Mirrors what it does
* Does what it is expected to do - _No unexpected solutions_
* Complies with known patterns
* Clean from „dirt” and pollution - _Boy Scout Rule: Leave it clean_
* Error free - _Makes hard for bugs to hide_

### Main Rules

* One code part implements one thing - _block, method, class, package, compilation unit_
* Implement things in a correct part - _misplaced responsibility_
* Meaningful names \(business meaning\)
* No magic numbers \(and strings and booleans\)
* No code repetition - _One thing is implemented once, one information is written once_
* Expected behavior
  * "Least astonishment"
  * Count of WTFs :-\)
  * No arbitrary solutions
  * Use known conventions and patterns

> Clean code = Expressiveness + modularity

### Code Quality

#### Possible Measurements

There is no overall and ultimate measure of code quality.

* Number of warnings
* Static code checkers - _CheckStyle, FindBugs, PMD, Sonar, ..._
* Complexity - _Cyclomatic complexity_
* Code smell
* Unit test coverage

![](../../.gitbook/assets/code-quality-wtfs.png)

### Developer Precisity

* Be precise
* Think
* Do not be careless
* Do not be arbitrary
* Be consequent

### Code Smell

* The feeling that something is not yet good with the code

### Issues

#### Avoid dogmatic style

* Always interfaces
* Always accessors/mutators \(getters/setters\)
* Structured programming: Only one return
* Mandatory comments -no comments needed for private methods

Example: Bad: Dogmatic style

```java
// Dogmatic comment results obvious comment
// Dogmatic getters/setters

/**
* Getter of {@link #_inputSource}.
* @return {@link #_inputSource}
*/
public final InputSource getInputSource() {
    return _inputSource;
}

public final void parse(final String[] configs, final String configPath, final boolean flushAfterParse) {
    if (getInputSource() != null) { }
}
```



