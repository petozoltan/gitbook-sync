---
description: 2023.07.14
---

# Don't Feed the Monsters

Every solution we introduce to the code comes at a price. Frameworks, layers, queues, architectural decisions, third-party tools, class hierarchies, models, techniques, and our own design ideas.

The price is that they will affect our coding. They will change it. Change from what?

All we need to do is to focus on the business logic. The user requirements. We should understand it, we should implement it, and the code should reflect it. This is called _clean code_.

But the technical solutions we add will _distract_ us from the business logic. We will spend an increasing amount of time writing code that is solely required by those frameworks and solutions and which has nothing to do with the user requirements.

> We must "feed" our creatures like slaves. And they are hungry!

Imagine just a simple class hierarchy. After introducing it we will have to create more and more classes and interfaces to satisfy the hierarchy and the compiler. We will have to create more and more overridden methods or split the code into more abstract methods to avoid overriding.

But remember, professional software development is not a Tamagotchi game. We don't have to do this. But how can we avoid having these hungry monsters?

<figure><img src="../.gitbook/assets/Tamagotchi s-l500 PSX.jpg" alt="" width="155"><figcaption></figcaption></figure>

### Requirements

We should investigate every solution and design decision before introducing them.&#x20;

The first and most important question: Are they required by the user requirements or can they be derived from them? In other words, do they implement a requirement at all? Or are they only a possibility or a "matter of taste"?

{% hint style="success" %}
Focus always on the business requirements and not on the solutions.
{% endhint %}

### Price–Benefit Balance

The second question is: Is it worth introducing a certain solution? Do we want to pay the cost for the benefit it brings? By cost I mean the _cost of maintenance_.

And this is where software development seems to fail. We have methods for everything: project management, build, delivery, code checking, etc.&#x20;

{% hint style="warning" %}
Software management never estimates the maintenance cost of the design decisions.
{% endhint %}

Yes, we estimate each task we implement. But we never compare implementing a task _with or without_ a certain technology. We have a blind spot for this. We never talk about this.

<figure><img src="../.gitbook/assets/Little.jpg" alt="" width="375"><figcaption></figcaption></figure>
