# Duplication

One of the "enemies" of clean code.

### Cases of duplication

* Copy-pasted parts
* Duplicated logic - _something implemented more times on different ways_
* Duplicated values or information - _literals or constants_

### Avoid inline implementation

This is also a _misplaced responsibility_!

* Not reusable - Leads to duplication
* Different implementations
* Not testable
* Refactor it

### DRY Principle

* Don't repeat yourself \(Kent Beck\)

Example: Refactor inline implementation

![](../../.gitbook/assets/refactoring-inline-implementation.png)

Example: Bad: Duplication causes incorrect intention

```java
// It suggests that it is a branching, but it is only a duplicate
// It differs only in the input value, which is implemented inline

public boolean isMultipleOriginAllowedForCountry(SearchFlightsForm form) {
    if (GstUserType.INTERNAL == userHelper.getCurrentUserUserType()) {
        return isCountryInTheListOfAllowedMultipleOrigins(form.getPos().getCode());
    } else {
        return isCountryInTheListOfAllowedMultipleOrigins(userHelper.getCurrentUserPos());
    }
}
```

Example: Good: No duplicates, correct intention

```java
public boolean isMultipleOriginAllowedForCountry(SearchFlightsForm form) {
    return isCountryInTheListOfAllowedMultipleOrigins(getPosOfUser(form));
}

// Extracted funtionality can be tested too
private String getPosOfUser(SearchFlightsForm form) {
    return GstUserType.INTERNAL == userHelper.getCurrentUserUserType() ? 
            form.getPos().getCode() : userHelper.getCurrentUserPos();
}
```

Example: Bad: Duplicated implementation with differences

```java
// Cause: laziness of the developer
// Cannot be found by a code checker
// Blocks the development and the refactoring too

public final void parse(final String[] configs, final String configPath, final boolean flushAfterParse) {
    final FileLocator locator = new FileLocator();
    try {
        if (getInputSource() != null) {
            final EdifactParser parser = new EdifactParser(getInputSource(), getHandler());
            final String extendedConfigPath = StringUtils.isEmpty(configPath) ? "" : configPath + CharacterConstant.SLASH;
            for (final String config : configs) {
                final File grammarFile = locator.locate(extendedConfigPath + config + ".xml");
                parser.addConfig(new Config(config, grammarFile));
            }
            parser.convert();
            if (flushAfterParse) {
                getHandler().flush(true);
            }
        }
    } catch (final IOException e) {
        throw new ExtendedRuntimeException(e);
    } catch (final ExtendedException e) {
        throw new ExtendedRuntimeException(e);
    } finally {
        locator.releaseAll();
    }
}

public final void parse(final Config[] configs, final boolean flushAfterParse) {
    final FileLocator locator = new FileLocator();
    try {
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
    } catch (final IOException e) {
        throw new ExtendedRuntimeException(e);
    } catch (final ExtendedException e) {
        throw new ExtendedRuntimeException(e);
    } finally {
        locator.releaseAll();
    }
}

// Other clean code issues in this example:
// - Methods are doing more than one thing
// - Inner dependency
// - Not expressive validity check
```

Example: Bad: Duplicates differ only in values

```java
// Bad intention: similar methods with very different names - how can be that?
// Methods do what they tell but you CANNOT SEE it
// It contains another duplication which can be expensive (e.g. database access)

private void fillOutCountriesForMultipleOrigin() {
    getSegments().get(0).setOrigin(countryAutoCompleteHelper.getCountryItemForAiportCode(getPosForMultipleOrigin()));
    if (JourneyType.OPEN_JAW.equals(getJourneyType())) {
        getSegments().get(1).setDestination(countryAutoCompleteHelper.getCountryItemForAiportCode(getPosForMultipleOrigin()));
    }
}

private void removeCountriesForNormalFlights() {
    getSegments().get(0).setOrigin(null);
    if (JourneyType.OPEN_JAW.equals(getJourneyType())) {
        getSegments().get(1).setDestination(null);
    }
}
```

Example: Good: Refactor value differences to input parameters

```java
// Methods do what they tell and you CAN SEE it

private void fillOutCountriesForMultipleOrigin() {
    setCountryForSegments(countryAutoCompleteHelper.getCountryItemForAiportCode(getPosForMultipleOrigin()));
}

private void removeCountriesForNormalFlights() {
    setCountryForSegments(null);
}

private void setCountryForSegments(AirportCityCodeItem country) {
    getSegments().get(0).setOrigin(country);
    if (JourneyType.OPEN_JAW.equals(getJourneyType())) {
        getSegments().get(1).setDestination(country);
    }
}

// It is not yet clean: magic numbers
// It is not yet clean: why only two segments?
```



