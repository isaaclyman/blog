---
title: "Lyman's Law"
categories: ["development"]
date: 2017-08-19T06:54:57-06:00
draft: false
genre: "Technology"
tags: ["code quality"]
---

A pretty-darned-optional part of being a software developer is getting a generally-applicable principle (a "law") named after yourself. Most of the time, it seems, this happens unintentionally--the law's originator doesn't necessarily foresee it becoming a pithy and oft-repeated internet adage. But if I could choose a principle to call "Lyman's Law," I think it might be this one:

> Code accompanied by unit tests will have a higher standard of code quality than code written without unit tests, even if the unit tests themselves are not taken into account.

<sup>If someone else has claimed this law already, feel free to point me in their direction so I can give them credit.</sup>

This is an argument for writing unit tests--or requiring your team to write unit tests--in situations where you don't feel that the unit tests themselves will add much value. Why? Because code written for testability is usually more modular, more loosely-coupled, more interface-driven, more composable and *more correct* than code written for suitability alone.

This has become significant to me as I've worked on a [legacy codebase](https://softwareengineering.stackexchange.com/a/122024) written without testability in mind. All the data is stored in a giant global object, no code is shared, there are reams of dead code lying about, UI and logic are tightly coupled, and much of the logic is nested seven or eight levels deep. In short, the [Cthulhu](https://en.wikipedia.org/wiki/Cthulhu#Description) of software projects. It's occurred to me more than once that one of the best ways to avoid this catastrophe would have been to instruct the team who built it to write unit tests. Arguably, they could have written bad unit tests and left the code in much the same state it's currently in. But it would have taken so much more cognitive effort to do so than to break down and modularize their code that one would hope they'd choose the latter.

If you're feeling so inclined, I'm sure you could provide a code snippet showing me that testable code can still be terrible code. You're not wrong. But untestable code *cannot* be good code. Therefore, unit-tested code will generally be of higher quality than untested code.

<sup>If you're incredulous about this claim, here's a thought exercise: ask yourself what traits may make a class or method untestable. Then determine what relationship these traits have with generally-accepted principles of code quality.</sup>

You may say that there's a difference between *untested* code and *untestable* code. I say the difference is mostly academic. If testability is not an explicit goal of the code, the developer will almost always take the path of least resistance (or, at the very least, make several small mistakes) and build in a way that makes it impossible or prohibitively difficult to add unit tests without refactoring.

To summarize my thesis: unit tests love code quality. The easiest thing to test is a loosely-coupled pure function with predictable outputs and a simple interface--and all these adjectives are hallmarks of clean code.

If you have something to add, please share your thoughts in the comment section.
