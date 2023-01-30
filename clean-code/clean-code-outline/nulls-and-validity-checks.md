# Nulls and Validity Checks

### Avoid NullPointerExceptions \(NPE\)

* Check at the beginning - _Unhappy path, Happy path_
* Consider using helper methods
* Check each object which is de-referenced in the method - and only these ones

Example: Bad: Null check at the wrong place

```java
void doSomething(MyClass input) {
    if(input != null) { // Unnecessary here
        doStuff(input);
    }
}

void doStuff(MyClass input) {
    input.setData(10); // Would be necessary here
}
```

Example: Good: Null check always and only when dereferencing

```java
void doSomething(MyClass input) {
    doStuff(input);
}

void doStuff(MyClass input) {
    if(input == null) {
        return;
    }
    input.setData(10);
}
```

### Defensive Programming

Also known as Secure Programming. A larger topic, but some elements:

#### Inputs

* Never trust data coming from outside - _user input, external systems_
* Fail early, Fail clean
* Create and use immutable types

#### Outputs

* Do not modify a data through getters
* Prevent it if possible - _unmodifiable collections_
* Create and use immutable types

Example: Bad: Unclear validity check

```java
// What to do when input source is null?
// Why is the entire content indented?
public final void parse(final Config[] configs, final boolean flushAfterParse) {
    if (getInputSource() != null) {
        final EdifactParser parser = new EdifactParser(getInputSource(), getHandler());
        for (final Config config : configs) {
            parser.addConfig(config);
        }
        parser.convert();
        if (flushAfterParse) {
            getHandler().flush(true);
        }
    }
}
```

Example: Good: Validity check at the beginning

```java
public final void parse(final Config[] configs, final boolean flushAfterParse) {
    // Unhappy path
    if (getInputSource() == null) {
        return; // Do nothing, return default or throw exception
    }
    // Happy path or Normal flow
    final EdifactParser parser = new EdifactParser(getInputSource(), getHandler());
    for (final Config config : configs) {
        parser.addConfig(config);
    }
    parser.convert();
    if (flushAfterParse) {
        getHandler().flush(true);
    }
}
```

### Parameters

* Do not pass explicitly null - _it is a "cheating", \_allow it with an overloaded method_

### Unit Test of Inputs

* Unit test will nulls and empty values in all possible ways
  * null object
  * entire collection or array is null
  * collection or array element is null

### Error Handling

* Do not return null - _rather throw exception_

> Things must not be multiplied beyond necessity. The simplest solution is the best. \(Occam’s Razor\)



