# Methods

### Rules

* "Small" - _Not an exact rule_
* Do only one thing - _even small methods may do more things!_
* One level of abstraction - _See Law of Demeter later_
* No unexpected behavior \(side effects\)
* No unexpected or not-understandable input and return values
* No or the least possible dependencies
* Avoid inline implementation - _put it always in a separate method_
* Set visibility modifiers precisely - _For the compiler and for the reader too_
* Check parameter validity at the beginning - _Item 38 in Effective Java \(2nd Edition, Joshua Bloch, 2008\)_
* Prevent overriding non-abstract methods - _Item 17 in Effective Java \(2nd Edition, Joshua Bloch, 2008\)_

Example: Bad: Unexpected behavior

```java
boolean checkPassword(String pwd) {
    if( pwd.equals(„secret”) ){
        createSession(); // Unexpected side effect
        return true;
    } else {
        return false;
    }
}
```

Example: Bad: Unintentional return values

```java
    int createProcess();

    // Which one is correct?
    errorCode = createProcess()
    processNumber = createProcess()
    processCount = createProcess()
    createdInMillis = createProcess()
```

Example: Bad: Method doing more than one thing

```java
// Are the lines in the proper order?
public synchronized void flush() throws IOException {
    getContentBuffer().flush();
    IOUtils.copy(new StringReader(getContentBuffer().getBuffer().toString()), getBufferedWriter());
    getBufferedWriter().flush();
    contentBuffer = new StringWriter();
}
```

Example: Good: Methods doing one thing

```java
// Method complies with the contract
@Override // This is also important, not only for the compiler
public synchronized void flush() throws IOException {
    flushMyBuffer();
    getBufferedWriter().flush();
}

private synchronized void flushMyBuffer() throws IOException {
    contentBuffer.flush();
    IOUtils.copy(new StringReader(getContentBuffer().getBuffer().toString()), getBufferedWriter());
    contentBuffer = new StringWriter();
}

// Now it is clear that it has two buffers. Is is a good solution?
// Clean code is not the final goal, it is a way to the goal:
// is the code correct?
```

Example: Bad: Method doing more than one thing _\(from the book\)_

```java
// It does three things
public void pay() {
    for (Employee e : employees) {
        if (e.isPayday()) {
            Money pay = e.calculatePay();
            e.deliverPay(pay);
        }
    }
}
```

Example: Good: Methods doing one thing \(from the book\)

```java
public void pay() {
    for (Employee e : employees) {
        payIfNecessary(e);
    }
}

private void payIfNecessary(Employee e) {
    if (e.isPayday()) {
        calculateAndDeliverPay(e);
    }
}

private void calculateAndDeliverPay(Employee e) {
    Money pay = e.calculatePay();
    e.deliverPay(pay);
}
```

Example: Bad: Side effect: modifying the input parameter

```java
// Incorrect name
private SelectedDirectionDTO createSelectedOption(OptionDTO option, String fareFamily) {

    SelectedDirectionDTO so = new SelectedDirectionDTO();
    so.setId(option.getId());
    so.setOrigin(option.getOrigin());
    so.setOriginCountry(option.getOrginCountry());
    so.setDestination(option.getDestination());
    so.setDepartureDate(option.getDepartureDate());
    so.setDepartureTime(option.getDepartureTime());
    so.setArrivalDate(option.getArrivalDate());
    so.setArrivalTime(option.getArrivalTime());
    so.setMultipleOrigin(option.isMultipleOrigin());
    so.getFlights().addAll(option.getFlights());

    // Non-standard TODO comment
    // Not informative comment
    //FB_TODO: the code from here might need changes
    // Negative condition first: harder to understand
    if (!moreOptions) {
        // Inline implementation
        for (RoutingFareDTO cFare : option.getFares()) {
            if (routingFareMatches(fareFamily, cFare)) {
                so.setFare(cFare);
            }
        }
    } else {
        // Inline implementation
        String fam = famMoreOptionMapping.get(fareFamily);
        if (fam != null) {
            for (RoutingFareDTO fare : option.getFares()) {
                if (fam.equalsIgnoreCase(fare.getCompartment())) {
                    so.setFare(fare);
                    // Modifying the input parameter!
                    so.getFare().setFareFamily(fareFamily);
                }
            }
        }
    }
    return so;
}
```

### Avoid Bad Input Parameter Types

* Object
* String for non-textual types
* boolean for switches - _use constants or enum instead_

### Program to Methods

Stateless, independent methods:

* Prefer return values to modifying input variables
* Prefer methods that depend only on the input parameters -No configuration parameters or data mining inside
* Independent = easily testable

At the end of the method calls there should always be a method that depend only on the input parameter and whose only result is the return value \(or exception\).

### Overloading

* Use overloading only for convenience
* For example for default values
* Do not use it for hiding differences
* They should call each other - _code smell if they don't_

### Hiding

* Hide irrelevant details in a separate method
* Do not hide relevant details in a separate method

Example: Bad: Overloads and Hiding

```java
// Overloads doing different things
// relevant details are hidden (what lists are created)
List<Integer> scores = initScores(10, 0);
List<Integer> scores = initScores(10);
```

Example: Good: No overloads and Hiding

```java
// Method intention is expressed in their names
// only irrelevant details are hidden (how lists are created)
List<Integer> scores = createListWithEqualNumbers(10, 0);
List<Integer> scores = createListWithDifferentNumbers(10);
```

### Two types of methods

* "Coordinator" or "orchestrator"
* "Technical" or "Algorithm"

Example: Good: Types of methods

```java
// Orchestrator method - Easy to read - Business logic
public void modifySomething(Something s) {
    s.setAnything( s.getThis(), s.getThat() );
    if( s.isBig() ) {
        s.setSomethingElse( DEFAULT_SOMETHING_ELSE );
    }
}

// Algorithm method - Easy to test
public Anything calculateAnything(This this, That that) {
    return this.getCount() * that.getSize();
}
```

How to use these types:

* Do not mix business lines with technical lines
* Do not pollute the code with technical details
* Hide irrelevant details
* Do not hide relevant details

Example: Bad: Pollution by repeating irrelevant technical details

```java
@Override
public List<DeadlineReminderMessageDTO> loadOptionDeadlineRemindersByPoses(List<String> gdUserPoses) {
    UriComponentsBuilder componentsBuilder = UriComponentsBuilder.fromHttpUrl(GSP_ROOT_URI + SpsRestEndpoint.OPTION_DEADLINE_REMINDERS_GD.getValue());
    componentsBuilder.queryParam("gdUserPoses", gdUserPoses.toArray());
    ResponseEntity<List<DeadlineReminderMessageDTO>> responseEntity = restTemplate.exchange(
            componentsBuilder.build().toString(),
            HttpMethod.GET, 
            null, 
            new ParameterizedTypeReference<List<DeadlineReminderMessageDTO>>() {}, 
            Collections.emptyMap());
    return responseEntity.getBody();
}

@Override
public List<DeadlineReminderMessageDTO> loadNameDeadlineRemindersByPoses(List<String> gdUserPoses) {
    UriComponentsBuilder componentsBuilder = UriComponentsBuilder.fromHttpUrl(GSP_ROOT_URI + SpsRestEndpoint.NAME_DEADLINE_REMINDERS_GD.getValue());
    componentsBuilder.queryParam("gdUserPoses", gdUserPoses.toArray());
    ResponseEntity<List<DeadlineReminderMessageDTO>> responseEntity = restTemplate.exchange(
            componentsBuilder.build().toString(), 
            HttpMethod.GET, 
            null, 
            new ParameterizedTypeReference<List<DeadlineReminderMessageDTO>>() {}, 
            Collections.emptyMap());
    return responseEntity.getBody();
}

@Override
public List<DeadlineReminderMessageDTO> loadTicketingDeadlineRemindersByPoses(List<String> gdUserPoses) {
    UriComponentsBuilder componentsBuilder = UriComponentsBuilder.fromHttpUrl(GSP_ROOT_URI + SpsRestEndpoint.TICKETING_DEADLINE_REMINDERS_GD.getValue());
    componentsBuilder.queryParam("gdUserPoses", gdUserPoses.toArray());
    ResponseEntity<List<DeadlineReminderMessageDTO>> responseEntity = restTemplate.exchange(
            componentsBuilder.build().toString(),
            HttpMethod.GET, 
            null, 
            new ParameterizedTypeReference<List<DeadlineReminderMessageDTO>>() {}, 
            Collections.emptyMap());
    return responseEntity.getBody();
}
```

Example: Good: No repeating technical details

```java
import static com.lhsystems.sales.gst.services.spsaccessor.rest.SpsRestEndpoint.*;

@Override
public List<DeadlineReminderMessageDTO> loadOptionDeadlineRemindersByPoses(List<String> gdUserPoses) {
    return loadDeadlineRemindersByPoses(OPTION_DEADLINE_REMINDERS_GD, gdUserPoses);
}

@Override
public List<DeadlineReminderMessageDTO> loadNameDeadlineRemindersByPoses(List<String> gdUserPoses) {
    return loadDeadlineRemindersByPoses(NAME_DEADLINE_REMINDERS_GD, gdUserPoses);
}

@Override
public List<DeadlineReminderMessageDTO> loadTicketingDeadlineRemindersByPoses(List<String> gdUserPoses) {
    return loadDeadlineRemindersByPoses(TICKETING_DEADLINE_REMINDERS_GD, gdUserPoses);
}

private List<DeadlineReminderMessageDTO> loadDeadlineRemindersByPoses(SpsRestEndpoint endpoint, List<String> gdUserPoses) {
    UriComponentsBuilder componentsBuilder = UriComponentsBuilder.fromHttpUrl(GSP_ROOT_URI + endpoint.getValue());
    componentsBuilder.queryParam("gdUserPoses", gdUserPoses.toArray());
    return loadDeadlineReminderMessages(componentsBuilder);
}

private List<DeadlineReminderMessageDTO> loadDeadlineReminderMessages(UriComponentsBuilder componentsBuilder) {
    ResponseEntity<List<DeadlineReminderMessageDTO>> responseEntity = restTemplate.exchange(
            componentsBuilder.build().toString(),
            HttpMethod.GET, 
            null, 
            new ParameterizedTypeReference<List<DeadlineReminderMessageDTO>>() {}, 
            Collections.emptyMap());
    return responseEntity.getBody();
}
```

### Method Smells

* Passing this to a method _- it could be implemented with more, smaller and readable classes._

> If you can mix a method's lines and it still compiles, it probably does more things. \(Zoltan Peto :-\)



