# Types

> The goal of typed languages is to pull issues from run time to compile time.

### Rules

* Use types
* Do not use String for non-textual values
* Do not use Strings for dates - _it is always formatted!_
* Avoid using boolean parameters - _hard to read, "magic numbers"_
* Create exception types instead of error codes

### Enums

* Enums are static constants
* You can static import enums to shorten the code
* Enums are created threadsafe
* Always use enums for a finit set of constants
* Use enum to map information
* Prefer enums to maps
* Prefer enums to switches
* Enums cannot have a parent class but can implement interfaces

Example: Bad: Implementation with collections and procedures

```java
public final class ContractFormatter implements Serializable {

    // They belong to formatFareFamily(), low cohesion
    // Misplaced constants
    // Duplications: they are defined sever times again and again...
    private static final String FORMATTED_FIRST_CLASS_FAM = "First";
    private static final String FORMATTED_BUSINESS_FAM = "Business";
    private static final String FORMATTED_ECONOMY_FAM = "Economy";
    private static final String FIRST_FAM = "FIRST";
    private static final String BUSINESS_FAM = "BUSINESS";
    private static final String ECONOMY_FAM = "ECONOMY";
    private static final String FORMATTED_ECONOMY_SAVER_FAM = "Economy Saver";
    private static final String ECOSAVER_FAM = "ECOSAVER";
    private static final String LIGHT_FB = "LIGHT_BUNDLE";
    private static final String CLASSIC_FB = "CLASSIC_BUNDLE";
    private static final String BUSINESS_FB = "BUSINESS_BUNDLE"; //FB_TODO: chage to final name
    private static final String FORMATTED_LIGHT_FB = "Light";
    private static final String FORMATTED_CLASSIC_FB = "Classic";
    private static final String FORMATTED_BUSINESS_FB = "Business"; //FB_TODO: chage to final name

    // Simple property implemented as a collection
    // It belongs to isFareBundle(), low cohesion
    private static final Set<String> fareBundleStrings = ImmutableSet.of(LIGHT_FB, CLASSIC_FB, BUSINESS_FB);

    public boolean isFareBundle(String famOrBundle) {
        return fareBundleStrings.contains(famOrBundle);
    }

    // Simple mapping implemented as a procedure
    public String formatFareFamily(String famOrBundle) {
        String fareFamily = famOrBundle;
        switch (famOrBundle) {
        case ECOSAVER_FAM:
            fareFamily = FORMATTED_ECONOMY_SAVER_FAM;
            break;
        case ECONOMY_FAM:
            fareFamily = FORMATTED_ECONOMY_FAM;
            break;
        case BUSINESS_FAM:
            fareFamily = FORMATTED_BUSINESS_FAM;
            break;
        case FIRST_FAM:
            fareFamily = FORMATTED_FIRST_CLASS_FAM;
            break;
        case LIGHT_FB:
            fareFamily = FORMATTED_LIGHT_FB;
            break;
        case CLASSIC_FB:
            fareFamily = FORMATTED_CLASSIC_FB;
            break;
        case BUSINESS_FB:
            fareFamily = FORMATTED_BUSINESS_FB;
            break;
        default:
            break;
        }
        return fareFamily;
    }
}
```

Example: Good: Information and mapping as enum

```java
import static com.lhsystems.sales.gst.common.domain.FareCategory.*;

public enum FareCode {

    ECOSAVER(FAMILY, "Economy Saver"),
    ECONOMY(FAMILY, "Economy"),
    BUSINESS(FAMILY, "Business"),
    LIGHT_BUNDLE(BUNDLE, "Light"),
    CLASSIC_BUNDLE(BUNDLE, "Classic"),
    BUSINESS_BUNDLE(BUNDLE, "Business"),
    FIRST(CLASS, "First");

    private FareCategory category; // Property
    private String displayInContract; // Mapping to another information

    private FareCode(FareCategory category, String displayInContract) {
        this.category = category;
        this.display = display;
    }

    public String getDisplay() {
        return display;
    }

    private boolean isFareBundle() {
        return category == BUNDLE;
    }
}
```

### Type Smells

* Do not pass parameters in a map

Example: Bad: Parameter map

```java
// Unintentional
// Shifts program errors to run time

void someMethod() {
    Map<String, Object> parameters = new HashMap<>();
    parameters.put("contract", contract);
    parameters.put("requestNr", 1);
    parameters.put("userId", user.getId());
    otherMethod(parameters);
}

void otherMethod(Map<String, Object> parameters) {
    Contract contract = (Contract) parameters.get("contract");
    Integer requestNr = (Integer) parameters.get("requestNr");
    Long userId = (Long) parameters.get("userId");
    ...
}
```

> Everything should be made as simple as possible, but not simpler. \(Albert Einstein\)



