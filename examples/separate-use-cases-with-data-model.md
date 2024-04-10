---
description: 2021.08.04
---

# Separate Use Cases With Data Model

## The Feature

In this example, we have to do the following:

* Do calculations with a pair of objects.
* Each of the two objects may be missing and we need to do different calculations in each case.
* We should do an extra step for each object in the pair if they are present.

It means, we have 3 main use cases:

1. both objects are present
2. the second one is missing
3. the first one is missing

Here we have our object types from the domain model. (For simplicity, getters and setters are omitted.)

{% tabs %}
{% tab title="Domain Model" %}
```java
class Value {
}

class Data {
    Optional<Value> first;
    Optional<Value> second;
}
```
{% endtab %}
{% endtabs %}

## Usual Implementation

Let's see, how we would usually implement it. (For simplicity, return values are omitted.)

{% tabs %}
{% tab title="Feature" %}
```java
class Feature {

    void calculate() {
        Collection<Data> dataCollection = loadData();
        calculate(dataCollection);
    }

    Collection<Data> loadData() {
        return ...;
    }

    void calculate(Collection<Data> dataCollection) {
        for (Data data : dataCollection) {
            if (data.first.isPresent() && data.second.isPresent()) {
                calculate(data.first.get(), data.second.get());
            } else if (data.first.isPresent() && !data.second.isPresent()) {
                calculate(data.first.get(), null);
            } else {
                calculate(null, data.second.get());
            }
        }
    }

    // Common code that contains branches

    void calculate(Value first, Value second) {

        if (first != null && second != null) {
            calculateBoth(first, second);
        } else if (first != null && second == null) {
            calculateFirst(first);
        } else {
            calculateSecond(second);
        }

        if (first != null) {
            registerFirst(first);
        }

        if (second != null) {
            registerSecond(second);
        }
    }

    void calculateBoth(Value first, Value second) {
        // ...
    }

    void calculateFirst(Value first) {
        // ...
    }

    void calculateSecond(Value second) {
        // ...
    }

    void registerFirst(Value first) {
        // ...
    }

    void registerSecond(Value second) {
        // ...
    }
}
```
{% endtab %}
{% endtabs %}

The primary problems with this code are:

* It contains the same `if` branches in two methods.
* The common code contains branches.
* It passes `null` values to methods.
* It uses `null` values to control the program flow.

Controlling the program flow with artificial `null` values is the [Insider Information](../data-processing/separate-use-cases.md#insider-information) antipattern. It means that _"if Value is null then the Data was empty"_. So it "finds out" the original situation, instead of receiving it as clear information.

The last two issues together also make it a _spaghetti code_: we pass the nulls _with the purpose_, to make branching in the other method. So the first method "continues" in the second one, instead of completing the branches.

## Separate Use Cases

To fix the above code we should follow the article [Separate Use Cases](../data-processing/separate-use-cases.md):

* Create branching for the use cases only once.
* Separate the implementations of the use cases.
* Call the real common code from the use cases, which do not contain branches.

{% tabs %}
{% tab title="Feature" %}
```java
class Feature {

    void calculate() {
        Collection<Data> dataCollection = loadData();
        calculate(dataCollection);
    }

    Collection<Data> loadData() {
        return ...;
    }

    // The only branching for the use cases

    void calculate(Collection<Data> dataCollection) {
        for (Data data : dataCollection) {
            if (data.first.isPresent() && data.second.isPresent()) {
                doUseCaseBoth(data.first.get(), data.second.get());
            } else if (data.first.isPresent() && !data.second.isPresent()) {
                doUseCaseFirst(data.first.get());
            } else {
                doUseCaseSecond(data.second.get());
            }
        }
    }

    // The use cases

    void doUseCaseBoth(Value first, Value second) {
        calculateBoth(first, second);
        registerFirst(first);
        registerSecond(second);
    }

    void doUseCaseFirst(Value first) {
        calculateFirst(first);
        registerFirst(first);
    }

    void doUseCaseSecond(Value second) {
        calculateSecond(second);
        registerSecond(second);
    }

    void calculateBoth(Value first, Value second) {
        // ...
    }

    void calculateFirst(Value first) {
        // ...
    }

    void calculateSecond(Value second) {
        // ...
    }

    // The real common code, without branching

    void registerFirst(Value first) {
        // ...
    }

    void registerSecond(Value second) {
        // ...
    }
}
```
{% endtab %}
{% endtabs %}

## Separate Data Creation and Processing

But there are more subtle problems with our code:

The calculation loads data.

* It is not clear what is the input of the calculation.
* It is not clear when the input data is complete.

The use cases are actually defined by the data, depending on which `Value` is missing. Why not reflect them directly in the data? In other words, we could define the use cases earlier, before the calculation starts. The calculation could contain only the implementations for the use cases.

For this, we create data transfer objects that clearly contain the data by use cases. And we add an extra step between the data loading and the calculation that creates these DTOs.

{% tabs %}
{% tab title="Feature" %}
```java
class ValuePair {

    Value first;
    Value second;

    ValuePair(Value first, Value second) {
        this.first = first;
        this.second = second;
    }
}

class ValuePairs {
    Collection<ValuePair> both = new ArrayList<>();
    Collection<Value> firsts = new ArrayList<>();
    Collection<Value> seconds = new ArrayList<>();
}

class Feature {

    void calculate() {
        Collection<Data> dataCollection = loadData();
        // Create the DTOs
        ValuePairs valuePairs = createValuePairs(dataCollection);
        calculate(valuePairs);
    }

    Collection<Data> loadData() {
        return ...;
    }

    // The only branching for the use cases

    ValuePairs createValuePairs(Collection<Data> dataCollection) {
        ValuePairs valuePairs = new ValuePairs();
        for (Data data : dataCollection) {
            if (data.first.isPresent() && data.second.isPresent()) {
                valuePairs.both.add(new ValuePair(data.first.get(), data.second.get()));
            } else if (data.first.isPresent() && !data.second.isPresent()) {
                valuePairs.firsts.add(data.first.get());
            } else {
                valuePairs.seconds.add(data.second.get());
            }
        }
        return valuePairs;
    }

    void calculate(ValuePairs valuePairs) {
        doUseCaseBoth(valuePairs.both);
        doUseCaseFirst(valuePairs.firsts);
        doUseCaseSecond(valuePairs.seconds);
    }

    // The use cases

    void doUseCaseBoth(Collection<ValuePair> boths) {
        for (ValuePair both : boths) {
            calculateBoth(both.first, both.second);
            registerFirst(both.first);
            registerSecond(both.second);
        }
    }

    void doUseCaseFirst(Collection<Value> firsts) {
        for (Value first : firsts) {
            calculateFirst(first);
            registerFirst(first);
        }
    }

    void doUseCaseSecond(Collection<Value> seconds) {
        for (Value second : seconds) {
            calculateSecond(second);
            registerSecond(second);
        }
    }

    void calculateBoth(Value first, Value second) {
        // ...
    }

    void calculateFirst(Value first) {
        // ...
    }

    void calculateSecond(Value second) {
        // ...
    }

    // The real common code, without branching

    void registerFirst(Value first) {
        // ...
    }

    void registerSecond(Value second) {
        // ...
    }
}
```
{% endtab %}
{% endtabs %}

Note, how the `if` commands have disappeared from the `calculate()` method. Why don't we need branching here? Because we have to process _all_ use cases. No decisions are needed. Actually, this was done by the original code too, but it was "disguised" as a branching. So this new code is more expressive.

As a consequence of the new data structure, we could also re-organize the for-each loops, since we already get the distinct collections for the use cases.

## Create Data Model And Inputs/Outputs

What we really did in the previous step is that we created a _data model for the feature_. We also made the new data as a clear input of the calculation.

Now it's time to re-organize our code into the proper units.&#x20;

I suggest creating a sub-package called model and put the DTOs and their factories here. I also suggest naming the factory classes exactly after the data classes they create.

Additionally, `ValuePairs` could be made less mutable and created clearly by a constructor. This would also better express and separate the use cases.

{% tabs %}
{% tab title="Feature" %}
```java
package feature;

public class Feature {

    private ValuePairsFactory valuePairsFactory;
    private Calculator calculator;

    public void calculate() {
        Collection<Data> dataCollection = loadData();
        ValuePairs valuePairs = valuePairsFactory.createValuePairs(dataCollection);
        calculator.calculate(valuePairs);
    }

    private Collection<Data> loadData() {
        return ...;
    }
}
```
{% endtab %}

{% tab title="Data Model" %}
```java
package feature.model;

public class ValuePair {

    Value first;
    Value second;

    public ValuePair(Value first, Value second) {
        this.first = first;
        this.second = second;
    }
}

public class ValuePairs {

    Collection<ValuePair> both;
    Collection<Value> firsts;
    Collection<Value> seconds;

    ValuePairs(
            Collection<ValuePair> both,
            Collection<Value> firsts,
            Collection<Value> seconds) {
        this.both = both;
        this.firsts = firsts;
        this.seconds = seconds;
    }
}
```
{% endtab %}

{% tab title="Data Factory" %}
```java
package feature.model;

public class ValuePairsFactory {

    public ValuePairs createValuePairs(Collection<Data> dataCollection) {
        return new ValuePairs(
                collectBoths(dataCollection),
                collectFirsts(dataCollection),
                collectSeconds(dataCollection));
    }

    private List<ValuePair> collectBoths(Collection<Data> dataCollection) {
        return dataCollection.stream()
                .filter(data -> data.first.isPresent() && data.second.isPresent())
                .map(data -> new ValuePair(data.first.get(), data.second.get()))
                .collect(Collectors.toList());
    }

    private List<Value> collectFirsts(Collection<Data> dataCollection) {
        return dataCollection.stream()
                .filter(data -> data.first.isPresent() && !data.second.isPresent())
                .map(data -> data.first.get())
                .collect(Collectors.toList());
    }

    private List<Value> collectSeconds(Collection<Data> dataCollection) {
        return dataCollection.stream()
                .filter(data -> data.second.isPresent() && !data.first.isPresent())
                .map(data -> data.second.get())
                .collect(Collectors.toList());
    }
}
```
{% endtab %}

{% tab title="Calculator" %}
```java
package feature;

public class Calculator {

    public void calculate(ValuePairs valuePairs) {
        doUseCaseBoth(valuePairs.both);
        doUseCaseFirst(valuePairs.firsts);
        doUseCaseSecond(valuePairs.seconds);
    }

    // The use cases

    private void doUseCaseBoth(Collection<ValuePair> boths) {
        for (ValuePair both : boths) {
            calculateBoth(both.first, both.second);
            registerFirst(both.first);
            registerSecond(both.second);
        }
    }

    private void doUseCaseFirst(Collection<Value> firsts) {
        for (Value first : firsts) {
            calculateFirst(first);
            registerFirst(first);
        }
    }

    private void doUseCaseSecond(Collection<Value> seconds) {
        for (Value second : seconds) {
            calculateSecond(second);
            registerSecond(second);
        }
    }

    private void calculateBoth(Value first, Value second) {
        // ...
    }

    private void calculateFirst(Value first) {
        // ...
    }

    private void calculateSecond(Value second) {
        // ...
    }

    // The real common code, without branching

    private void registerFirst(Value first) {
        // ...
    }

    private void registerSecond(Value second) {
        // ...
    }
}
```
{% endtab %}
{% endtabs %}

Of course, the package _must not_ be literally called "feature". Instead, it should have the actual feature name.

## Simpler Or Shorter?

You may say that the resulting code is pretty much longer than the original one. Yes, it's true. But how can it be better, and how can we say that it is simpler?

Think of the daily work of a programmer. We need to develop and modify features and use cases. Imagine that we need to do a change or fix a bug in one of the use cases.&#x20;

* How could we find it in the code, if it has no name? If it is just embedded somewhere?
* How could we find it, if it is implemented in more places? If it is "hiding" in more code parts?
* How could we modify it and be sure, we do not change something _else_ at the same time?

So, such code is hard to maintain and our changes will be prone to errors. A good code can be longer, but it is easier to find something in it, and it is _simpler_ to maintain.

Everything we implement is a deal: it has a price and a benefit. Yes, we pay an extra price to write clean and safe code. But we save many times more effort and problems with it, through the lifetime of the program. And that's why I not recommend using inheritance: the highest price with the lowest benefit. Did you notice that there is no inheritance in this example?

You can also think of the extra code that they were implicitly in the original code too, but it was not expressed, not visible. The extra code _had to be_ there but it wasn't.

Most of the new code lines contain names. And this is not a "by-product" of our refactoring. Having names is a _goal_. We use names to separate the parts and to find them.

Also, note that by writing more code lines we also have moved them into more small units. Each unit we created is _smaller_ _and simpler_ than the original code.

And remember, this is a simplified example. A real-life code is much more complicated. And if the parts of a complicated code are mixed and not named either, then we will have problems with maintaining that code.

![](../.gitbook/assets/Quotation-Albert-Einstein-Make-everything-as-simple-as-possible-but-not-simpler-8-73-34.jpg)
