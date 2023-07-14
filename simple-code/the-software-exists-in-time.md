---
description: 2023.07.14
---

# The Software Exists In Time

Another issue that may lead to a confusing code is that we tend to ignore that our source code exists in time. I don't say we forget it but we don't take it seriously enough, with all of its consequences.

### The code is continuously changing

One of the obvious goals of software development is that the program works correctly as specified. So the definition of _goodness_ is based on the correct and tested functionality. So far, so good.

But what do all the software developers in the world do each and every day?

They sit down to their computers and start modifying the code. They change the code that was written yesterday or last week or last month.

{% hint style="warning" %}
They modify the program that has worked well and has been tested!
{% endhint %}

So, is the above definition still good? I think it is not. It tells only that the software works correctly _now_. So we need to extend the project goal like this:

{% hint style="success" %}
The program should work correctly now and at any time in the future.
{% endhint %}

Why is it better? Because it has the consequence:

{% hint style="info" %}
We need to implement different features with the least possible dependencies.
{% endhint %}

Unfortunately, solutions like [OOP](../oop/do-not-use-inheritance.md), [frameworks](../oop/what-is-the-problem-with-inheritance.md), and [common code that is not common](separate-use-cases.md), create many unwanted dependencies in the code.

### Design for a long-term maintenance

Besides goodness, the other goal is the next deadline. All plans and estimations aim at the next deadline. The result is the following:

* It _may_ lead to quick & dirty programming.
* Technical debt is collected.
* It will seriously slow down the development and put future deadlines at risk.

It will be nearly impossible to work on technical debt later since we will always work on new features and bug fixes for future deadlines.

Everybody knows that the source code should be maintainable. But if we do not _plan_ it, it won't be.

{% hint style="success" %}
The goal is to maintain the software _for years_. The code must be maintainable.
{% endhint %}

As a consequence:

{% hint style="info" %}
We need to choose solutions that are easy to maintain.
{% endhint %}

And the "next deadline" sounds like a secondary goal, considering _all_ deadlines during the software's lifecycle.
