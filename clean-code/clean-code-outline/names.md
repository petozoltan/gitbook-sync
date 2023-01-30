# Names

### Rules

* Meaningful
* Intentional - _telling what it does_
* Readable, understandable
* Self-explanatory
* Not disinforming
* Pronounceable
* Consequent
* Do not force 'mind-mapping'

### Practice

* Names just repeat the types - _if types are correct and methods are small_
* The same object should have the same name when passed to other methods - _not always but usually_
* Prefer positive conditional names - e.g. avoid !isNot\(\)\_

### Some conventions

* Class name: noun
* Method name: verb
* Avoid prefixes and technical terms \(e.g. Abstract\)
* Name length corresponds scope length
* Old Enterprise JavaBeans - EJB
* Comply with: Java Code Conventions \(Sun, 1997\)

### EJB - Enterprise JavaBeans

* `private Foo foo` - _foo is a 'property' name_
* `public Foo getFoo()` - _the property name with a capital_
* `public void setFoo(Foo foo)`
* `public boolean isSomething()` - _also hasSomething\(\)_

Example: Bad: Names

```java
class DtaRcrd102 {

    // Not meaningful, not readable, not pronounceable
    Date genymdhms;
    Date modymdhms;
    String pszqint = "102";

    // Avoid prefixes and Hungarian notation
    String m_dsc;
    String strName;

    // Hard to read
    XYZControllerForEfficientStorageOfStrings con1;
    XYZControllerForEfficientHandlingOfStrings con2;

    // Disinforming
    void setName(String name) {
        m_dsc = name;
    }

    // Not informative
    void doCalculation() {

        // Too short names, Magic numbers
        for (int j=0; j<34; j++) {
            s += (t[j]*4)/5;
        }
    }
}
```

Example: Good: Names

```java
class Customer {

    private String description;
    private Date generationTimestamp;
    private Date modificationTimestamp;;
    private final String recordId = "102";
    int realDaysPerIdealDay = 4;
    const int WORK_DAYS_PER_WEEK = 5;
    int sum = 0;

    void setDescription(String description) {
        this.description = description;
    }

    int calculateWeeks() {
        for (int j=0; j < NUMBER_OF_TASKS; j++) {
            int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
            int realTaskWeeks = (realdays / WORK_DAYS_PER_WEEK);
            sum += realTaskWeeks;
        }
        return sum;
    }
}
```

Example: Bad: Not informative names

```java
// What does it really do?
assertThat(scores, is(StudentService.collectScores(STUDENT_LIST2)));
```

Example: Good: Informative names

```java
// Readable: "It creates an empty score list from an empty student list"
assertThat(emptyScoreList, is(StudentService.collectScores(STUDENT_LIST_EMPTY)));
```

Example: Bad: Not informative name of input parameter

```java
// What kind of input value is converted?
// It is not a 'find' but rather a 'convert'
private String findDeadlineType(int i) {
    String result;
    switch (i) {
    case 0:
        result = RK_FIRST_NAME_DEADLINE;
        break;
    case 1:
        result = RK_SECOND_NAME_DEADLINE;
        break;
    default:
        result = ""; //future values come here
        break;
    }
    return result;
}

// Best practice: Refactor to enum
```

Example: Bad: Confusing characters _\(From the book\)_

```java
    int a = l;
    if ( O == l )
        a = O1;
    else
        l = 01;
```

Example: Good: Name lengths correspond to scope

```java
// The class is one screen long
@Component
public class NameDeadlineReminderMessageCollector {

    @Autowired
    private DeadlineReminderMessagePnrFilter filter; // Used only in this class

    @Autowired
    private DeadlineReminderMessageSorter sorter; // Used only in this class

    @Transactional(readOnly = true)
    public List<DeadlineReminderMessage> collectDeadlineRemindersByAgency(String agencyInternalId) {
        return sorter.sort(filter.filter(findDeadlines(agencyInternalId), findPnrs(agencyInternalId)));
    }

    @Transactional(readOnly = true)
    public List<DeadlineReminderMessage> collectDeadlineRemindersByPoses(List<String> poses) {
        return sorter.sort(filter.filter(findDeadlines(poses), findPnrs(poses)));
    }
}
```



