---
description: 2023.07.14
---

# Consider the Maintenance Cost

### Software Estimation

The goal of software estimation is usually to tell this: which _specific_ features can we deliver on a _specific_ deadline?

But it does not consider the cost of _maintaining_ the code in the long term, which spans through deadlines.

### Look at the price tag

Imagine that we want to create a financial plan for our household. We want to know how much money we have and what we can buy.

Can we create this plan so that we do not care about the prices? Can we buy anything? Can we buy a new Lamborghini? Or even worse: can we buy an old second-hand car for the price of a new Lambo?

{% hint style="info" %}
We have to look at the price tags!
{% endhint %}

We have to do this in software estimation too.&#x20;

We never involve the maintenance cost in the decision when choosing a solution. We have a blind spot on it. So we end up paying a big price for a small benefit.&#x20;

### Why does the code have a maintenance cost?

Unfortunately, the code we write is not a _write-once-and-forget_ thing. We will have to modify the code in the future multiple times for some obvious reasons:

* Bug fixes. If there are errors in the code, we have to fix them.
* Change requests from the customer. We will surely get them and will have to do them.

Sadly, that's not all. The maintenance cost will get higher due to other reasons:

* The complexity of the code will increase during the frequent modifications.
* The code we write is simply not clear, and not readable enough.
* The solutions we have chosen are hard to maintain.&#x20;

These expensive solutions usually contain:

* Too many dependencies between the features that should be as independent as possible.
* Too many indirections, making the code less straightforward and less readable.

### Cost/benefit ratio

Of course, every solution we chose comes with a benefit too. But we should investigate the cost/benefit ratio before implementing it.

#### Unnecessary code

There is an alarming consequence of this "formula":

{% hint style="warning" %}
The cost/benefit ratio is infinitely high for the solutions which are _not necessary_.
{% endhint %}

For example, OOP and inheritance have very high maintenance costs, while they are not necessary. See here why: [Separate Data And Procedures](../oop/separate-data-and-procedures.md), [Do Not Use Inheritance](../oop/do-not-use-inheritance.md)

#### Overestimating the benefits

Be careful when estimating the benefit of a solution. We, programmers, are always enthusiastic about the solution itself, overestimating its benefit.

We typically create abstract, generic, and automated solutions, saying it will be good for future extensions. But they will never be good! We cannot foresee the future requirements that will enforce us to rewrite the existing code.

{% hint style="warning" %}
Do not implement a solution for unforeseen future requirements.
{% endhint %}

### How to decrease the maintenance cost?

I do not simply suggest to add the maintenance cost to the usual estimations.

Instead, we should decide whether we keep or drop a solution. Of course, this needs us to design and discuss the solutions before implementing them.

{% hint style="warning" %}
Avoid estimating the costs when it is too late—i.e. when it is already implemented.
{% endhint %}

### When and how to implement complex solutions?

More precisely when to choose a complex and expensive solution _for one specific feature within a larger software_?&#x20;

The answer is simple but it may be inconvenient:

{% hint style="info" %}
Treat complex solutions as distinct software.
{% endhint %}

* Sell it to the customer.
* Dedicate a team.
* Separate the code base.
* Specify, design, and document.
* Implement and test separately.
