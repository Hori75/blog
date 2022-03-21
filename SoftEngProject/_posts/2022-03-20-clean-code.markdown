---
layout: post
title:  "Clean Code"
author: hori75
date:   2022-03-20 21:00:00 +0700
background: '/images/code-quality.png'
excerpt_separator: <!--more-->
---

Is your code readable?
<!--more-->
On your first time learning to code or a new framework, you might not need to write the good code.
Why? Because it's for your learning only. When you start to work on a project with others,
you might be told to follow a guideline or a convention. When working with others, your work
must be reviewed by others or you must wrote your idea to communicate it with others.
This is might be done in other way, the thing is, the code should be readable by others to make it maintainable.

### What is Clean Code?

Clean code is a readable, maintanable, and well-written code. It has its following characteristics:

- Other developers could understand it quickly
- Don't have too many duplications
- Contains minimal classes and method, and
- Works as expected (obviously)

This characteristics then implies the code is readable and could be fixed quickly in case there is a semantic bug.

### Why it's needed?

As previously stated, when working with others, having a clean code makes life easier for the team.
Imagine you work on a poorly written code, the code is not formatted properly, there are too many methods or classes.
The easiest way is to ask someone who created the code. But, what if they already left the team for good.
This means that you need to decipher the code purpose and take a while to understand, and what if you forget it again.
That is why clean code was needed when working in teams, you also could do it on your own code and gain benefit from it.

### When to refactor/clean?

There are several principles on when or what to refactor. 

#### Don't Repeat Yourself (DRY)

As it said, you shouldn't create duplicate codes. 
In order to avoid duplication, you should create abstraction of the repeated process.
But sometimes, too much abstractions could make the code more unreadable.
This is the downside of this principle and the following principle is created to ease this.

#### Write Everything Twice (WET)/ Rule of Three

This principle gives more flexibility in order to prevent over abstractions.
You could write it twice but if you write the same thing the third time, you need to refactor.
Same as before, you could create abstraction of the repeated process.

#### You Aren't Gonna Need It (YAGNI)

When you write the code, the code should have its purpose in a workflow.
Otherwise, you actually aren't gonna need it and you should remove it.
By thinking this way, we could prevent unnecessary codes in the first place.

#### Keep It Simple Stupid (KISS)

A phrase from long time could be applied while writing the code.
If the implementation is really complex, you should think again to see if there is other simpler way.
Writing the simpler code means simpler workflow and could be checked easily for bugs.

#### Etc

Also, there are several times you might need to refactor the code

- refactor when adding new feature
- refactor when fixing bugs
- refactor in code review

### How to refactor/clean?

While cleaning the code, there are checklists to check whenther you have refactor it properly or not.

- Code should be cleaner (obviously)
- No new functionality from the changes
- Existing tests should pass

The work that needs to be done depends on reason refactoring is needed.
Might be to eliminate code duplication or to completely reimplement the flow.

Aside from cleaning from semantic mess, you could [literally] tidy the code by following a certain codestyle.
In that way, your codestyle is consistent and more readable.

### Conclusion

The principles of clean code are flexible and there aren't clear and strict rules.
but it should be implemented in order to have readable and maintainable code. 

### Reference

For more guides and techniques of refactoring, you could learn quickly from [Refactoring Guru](https://refactoring.guru/refactoring)

If you want a well written guideline and principles, you could read [Clean Code book by Robert C. Martin](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)

Thumbnail comic: [xkcd: Code Quality](https://xkcd.com/1513/)
