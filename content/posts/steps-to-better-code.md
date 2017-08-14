---
title: "Steps to better code"
categories: ["development"]
date: 2017-07-28T14:01:53-06:00
description: "A guide for beginners"
draft: false
genre: "Technology"
tags: ["beginners", "code quality"]
---

When you start out coding, you usually spend a year or two completely oblivious to the rules of “good code.” You may hear words like “elegant” or “clean” tossed around, but you can’t define them. That’s okay. For a programmer without any experience, there’s only one metric worth keeping tabs on: does it work?

Soon, though, you’ll need to raise your expectations. Good code doesn’t just _work._ It’s simple, modular, testable, maintainable, thoughtful. Some of these terms may apply to your code without you even knowing it, but probably not. If you’re lucky, your team carefully plans and architects its code solutions and guides you gently, trusting that you’ll develop an intuition for well-written software. If you’re not lucky, they [wince](https://xkcd.com/1513/) [or](https://xkcd.com/1695/) [complain](https://xkcd.com/1833/) every time they see your code. Either way, you can get a lot of mileage out of learning a few universal principles.

Take, for example, the _global variable_: any unscoped variable trivially accessible throughout the codebase. Suppose your app has a `username` variable that’s set when the user logs in and can be accessed from any function in the app just by referencing the variable name — that’s a global variable. Global variables are universally despised by influential bloggers and style guides, but most entry-level coders don’t understand why. The reason is — and pay attention, because this is the reason for almost all best practices in coding — that _it makes the code faster to write, but harder to understand_. In this case, a global variable makes it really easy to insert the user’s username into the app anywhere you want, which may mean fewer lines of code and fewer minutes between you and your next production release. That’s false comfort, though: you’ve sacrificed safety for convenience. If you discover a bug involving `username`, you will have to debug not just a single class or method, but the entire project. I’ll talk more about this later.

The difference between “good code” and “bad code” isn’t usually based on the way it affects _you_ as you write it. Code is always a shared resource: you share it with other open-source maintainers, or with the other developers on your team, or with the person who will have your job in the future, or with “future you” (who won’t have a clue what “present you” was thinking), or even just with “debugging you,” who is going through your fresh code looking for bugs and is hecka frustrated. All of these people will be grateful if your code makes sense. It will make their job easier and less stressful. In this way, writing good code is a form of professional courtesy.

If you’re still incredulous, read on — I’ll talk about several principles that lead to good code and try to justify each one.

#### Terms

Some quick definitions before we get started:

- _state:_ the data stored in memory as your program runs. Every variable you assign is part of the program’s state.
- _refactor:_ to change the code of a program without changing its behavior (as far as the user is concerned). The goal of refactoring is usually to make code simpler, more organized and easier to read.

#### 1 . [Separation of concerns](https://en.wikipedia.org/wiki/Separation_of_concerns)

A fair analogy for coding is writing a recipe. In simple recipes, each step depends on the one before it, and once all the steps are complete, the recipe is done. But if you’ve ever tried to follow a more complex recipe, you’ve probably experienced the stress of having two pots boiling on the stove, a plate spinning in the microwave, three kinds of vegetables half-chopped on a cutting board, and a smorgasbord of spice and herb shakers strewn across the countertop (and you can’t remember which ones you’ve already added).

Having another cook in the kitchen complicates the problem as often as it simplifies it. You waste time coordinating, handing things back and forth, and fighting over stovetop space and oven temperature. It takes practice to figure out how to do it well.

If you know you’re going to have several cooks in the kitchen, wouldn’t it be more efficient for the recipe to be split into mostly-independent sub-recipes? Then you could hand part of the recipe to each cook and they could work with as little interaction as possible. One of them is boiling water for pasta. One of them is chopping and cooking vegetables. One of them is shredding cheese. One of them is making sauce. And the points of interaction are clearly defined, so each of them knows when to hand off their work.

The worst form of code is like a simple recipe: a bunch of steps in order, each fully defined in the same space, and threaded from top to bottom. In order to understand it and modify it, you have to read the whole thing a couple of times. A variable on line 2 could affect an operation on line 832, and the only way to find out is to peruse the entire program.

A slightly better form of code is like having a second cook in the kitchen. You hand off some operations to other parts of the program, but your goal is mostly to reduce the complexity of the codebase, not necessarily to organize it. It’s an improvement, just not taken far enough.

The best form of code is like splitting a recipe into sub-recipes, usually called “modules” or “classes” in code. Each module is concerned with a single cohesive operation or piece of data. The vegetable chef shouldn’t have to worry about the sauce ingredients, and the person cooking pasta shouldn’t have to worry about the cheese grater. Their concerns are separated (hence, _separation of concerns_).

The benefits to this are significant. Suppose a coder needs to modify the program later — to make it gluten-free for a client with Celiac Disease or to add a seasonal vegetable. That coder will only need to read, understand and modify one small part of the program. If all of the code dealing with vegetables is contained in a single small class with a minimal interface, the coder never needs to worry that adding a vegetable will ruin the sauce.

The goal here is to make sure that, to make any given change, the coder has to think about as few parts of the program as possible, instead of all the parts at once.

#### 2 . [Global variables](https://en.wikipedia.org/wiki/Global_variable) (are bad)

Let’s jump back to your `username` variable. When you built the login form for your app, you realized you’d need to display the user’s username in a few places, like perhaps the header and the settings page. So you take the path of least resistance: you create it as a global variable. In Python, it’s declared with the `global` keyword. In JavaScript, it’s a property of the `window` object. It seems like a good solution. Anywhere you need to show the username, you just pop in the `username` variable and you’re on your way. Why aren’t all variables maintained like this?

Then things go sideways. There’s a bug in the code, and it has something to do with `username`. Despite the availability of an instant code search tool in most IDEs, this is going to take a while to fix. You’ll search `username` and there will be hundreds or thousands of results; some will be the global variable you set up at the beginning of the project, some will be other variables that also happen to be named `username`, and some will be the word “username” in a comment, class name, method name, and so forth. You can refine your search and reduce the amount of cruft, but debugging will still take longer than it should.

The solution is to put `username` where it belongs: inside of a container (e.g. a class or data object) that gets injected or passed as an argument to the classes and methods that need it. This container can also hold similar pieces of data — anything that’s set at login is a good candidate (but don’t store the password. Don’t ever store a password). If you’re so inclined, you can make this container immutable, so that once `username` is set, it can’t ever be changed. This will make debugging extremely easy, even if `username` is used tens of thousands of times in your app.

Coding this way will make your life easier. You’ll always be able to find the data you’re looking for, in exactly one place. And if you ever need to track when a piece of data is used or changed, you can add a getter or a setter and be on your way.

#### 3 . [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)

Let’s talk about relationships for a second.

Being in a relationship is good because of the companionship and support of your partner. Being in a relationship is bad because every time you meet someone new, or someone you haven’t seen in a long time, they’ll want to hear the story of how you two met. And that story is rarely as simple as “we struck up a conversation in the grocery store and got married the next day.” So you end up telling the same 15 minute long story a couple times per week, and that gets old really fast.

To make things worse, imagine that after several months you learn some new information about your love-at-first-sight story: you thought it was a happy accident, but it wasn’t accidental at all. A mutual acquaintance, after months of careful plotting, had successfully orchestrated that first “hello” and used subconscious suggestion to make you like each other. On the one hand, it worked out and you’re both happy. On the other hand, you’ve been telling a grossly incomplete story for months. When people find out what really happened, they may think that you lied to them (a white lie, perhaps, but still embarrassing).

In utter frustration at this turn of events, you create a web page with the most up-to-date version of the “how we met” story, then visit FedEx to print out a thousand business cards with a shortened link to the page. You mail one to everyone who has heard the old, now-obsolete story. And from now on, whenever someone asks how you met your partner, you will just pull the stack of business cards from your back pocket and hand them one. If the story ever changes, you can update the webpage and everyone will have access to it.

Not only is this a great way to mitigate one of the most difficult problems of relationships, but it’s the best way to code: code each operation (each algorithm, each presentation element, each interaction with an external interface) only once, and whenever another piece of code needs to know about that operation, refer back to it by name. _Every time you copy and paste code within your codebase, you should ask yourself if you’re doing something wrong._ If the “how the `LonelyUser` object got mapped to a `MarriedUser` object” story (or any other story) is told more than once, it’s time to refactor.

The goal is this: if an operation needs to change in some way, you should only have to modify a single class or method. This is quicker and far more reliable than trying to maintain several copies of the same code — it will take much longer to update all of them when changes are needed and, invariably, one or two of them will get left behind, causing bugs that are hard to diagnose.

#### 4 . [Hiding complexity](https://en.wikipedia.org/wiki/Information_hiding)

I have a car to sell you. It will take some training for you to learn how to use it.

To start the car, take red wire #2 and white wire #7 and touch them together while kicking the engine-rev pinwheel with your foot and pouring an appropriate amount of fuel into the injector, which you’ll find under the center console. Once the car has started, reach into the gearbox and push the layshaft into place against the first gear on the differential shaft. To accelerate, increase the flow of gasoline into the injector. To brake, hold your feet against the tires.

I hope you hate this car as much as I do. Now project that hatred onto code elements with over-complicated interfaces.

When you build a class or method, the first thing you write should be the _interface_: the part that a different piece of code (a caller) would need to know about in order to use the class or method. For a method, this is also called the _signature_. Every time you look up a function or class in API documentation (like on MDN or jquery.com), what you’re seeing is the interface — only what you need to know to use it, without any of the code it contains.

An interface should be simple but expressive. It should make sense in plain English, without expecting the caller to know about the order in which things happen, data that the caller isn’t responsible for, or global state.

This is a bad interface:

{{< highlight javascript >}}
function addTwoNumbersTogether(number1, number2, memoizedResults, globalContext, sumElement, addFn) // returns an array
{{< /highlight >}}

This is a good interface:

{{< highlight javascript >}}
function addTwoNumbersTogether(number1, number2) // returns a number
{{< /highlight >}}

If an interface can be smaller, it should be. If a value you’re providing explicitly could be inferred from other values, it should be. If a method has more than a few parameters, you should ask yourself if you’re doing something wrong (although you might make an exception for dependency injected constructors).

Don’t take this too far. If you’re setting and using global variables in order to avoid passing parameters to a function, you’re doing it wrong. If a method requires a lot of different pieces of data, try splitting it out into more specific functions; if that’s not possible, create a class specifically for passing this data around.

Remember that _all methods and data_ owned by a class but accessible outside of that class are part of its interface. This means you should make as many methods and fields private as you possibly can. In JavaScript, variables declared using `var`, `let`, or `const` are automatically private to the function they’re declared in, as long as you don’t return them or assign them to an object; in many other languages, there is a `private` keyword. This should be your best friend. Only make data public on a need-to-know basis.

#### 5 . Proximity

Declare things as close as possible to where they’re used.

Programmers’ instinctive urge to organize can work against them here. You may think an organized method looks like this:

{{< highlight javascript >}}
function () {
  var a = getA(),
      b = getB(),
      c = getC(),
      d = getD();

  doSomething(b);
  doAnotherThing(a);
  doOtherStuff(c);
  finishUp(d);
}
{{< /highlight >}}

`getA()` and its compatriots aren’t defined in this segment, but imagine that they return useful values.

In a small method like this, you may be forgiven for thinking the code is well-organized and easy to read. But it’s not. `d`, for some reason, is declared on line 4 even though it isn’t used until line 9, which means you have to read _almost the entire method_ to make sure it isn’t used anywhere else.

A better method looks like this:

{{< highlight javascript >}}
function () {
  var b = getB();
  doSomething(b);

  var a = getA();
  doAnotherThing(a);

  var c = getC();
  doOtherStuff(c);

  var d = getD();
  finishUp(d);
}
{{< /highlight >}}

Now it’s clear when a variable is going to be used: immediately after it’s declared.

Most of the time the situation isn’t so simple; what if `b` needs to be passed to both `doSomething()` and `doOtherStuff()`? In that case, it’s your job to weigh the options and make sure the method is still simple and readable (primarily by keeping it _short_). In any case, make sure you don’t declare `b` until immediately before its first use, and use it in the shortest possible code segment.

If you do this consistently, you’ll sometimes find that part of a method is completely independent from the code above and beneath it. This is a good opportunity to extract it into its own method. Even if that method is only used once, it will be valuable as a way to enclose all the parts of an operation in an easily understandable, well-named block.

#### 6 . Deep nesting (is bad)

JavaScript is known for an uncomfortable situation known as “callback hell”:

![](https://cdn-images-1.medium.com/max/1024/1*lDjW_AqCulDGWnMjyXHqag.jpeg)<figcaption>Via <a href="https://vimeo.com/131192407">https://vimeo.com/131192407</a>.</figcaption>

See that trail of `)};` running down the middle of the page? That’s the calling card of callback hell. It’s avoidable, but that’s a subject that plenty of other writers have already addressed.

What I want you to consider is something more like “if hell”.

{{< highlight javascript >}}
callApi().then(function (result) {
  try {
    if (result.status === 0) {
      model.apiCall.success = true;

      if (result.data.items.length > 0) {
        model.apiCall.numOfItems = result.data.items.length;

        if (isValid(result.data) {
          model.apiCall.result = result.data;
        }
      }
    }
  } catch (e) {
    // suppress errors
  }
});
{{< /highlight >}}

Count the pairs of `{` curly braces `}`. Six, five of which are nested. _That’s too many_. This block of code is hard to read, partially because the code is about to creep off the right side of the screen and programmers _hate_ horizontal scrolling, and partially because you have to read all the `if` conditions to figure out how you got to line 10.

Now look at this:

{{< highlight javascript >}}
callApi().then(function (result) {
  if (result.status !== 0) {
    return;
  }

  model.apiCall.success = true;

  if (result.data.items.length <= 0) {
    return;
  }

  model.apiCall.numOfItems = result.data.items.length;

  if (!isValid(result.data)) {
    return;
  }

  model.apiCall.result = result.data;
});
{{< /highlight >}}

That’s a lot better. We can clearly see the “normal path” for the code to follow, and only in abnormal situations does the code stray off into an `if` block. Debugging is much simpler. And if we want to add extra code to handle error conditions, it will be easy to add a couple of lines inside those `if` blocks (imagine if the `if` blocks in the original code had `else` blocks attached! The horror).

Also, I removed the try-catch block because you should never, ever, ever suppress errors. Errors are your friend, and without their help your application will be garbage.

#### 7 . [Pure Functions](https://en.wikipedia.org/wiki/Functional_programming#Pure_functions)

A pure function (or functional method) is simply a method that does not alter or depend on external state. In other words, for a given input, it will always provide exactly the same output, no matter what has changed outside of it, and application state will be completely unaffected by what happens inside of it. All pure functions have at least one argument and at least one return value.

This function is pure:

{{< highlight javascript >}}
function getSumOfSquares(number1, number2) {
  return (number1 * number1) + (number2 * number2);
}
{{< /highlight >}}

And this one is not:

{{< highlight javascript >}}
function getSumOfExponents(number1, number2) {
  scope.sum = Math.pow(number1, scope.exp) + Math.pow(number2, scope.exp);
}
{{< /highlight >}}

If you want to debug the first function, everything you need is right there. You can paste it into a separate environment, like jsfiddle or the browser console, and play with it until you find out what’s wrong.

If you want to debug the second function, you may have to dig through the entire program in order to make sure that you’ve found all the places where `scope.sum` and `scope.exp` are accessed. And if you ever want to move the function to another class, you’ll have to worry about whether it has access to all the same scope.

Not all methods can be pure; if your application didn’t have state, its usefulness would be limited. But you should write pure functions as often as possible. This will make your program easy to maintain and scale.

#### 8 . Unit Tests (are good)

Any class or method that’s more than a bare wrapper over other code — that is, any class or method that contains logic — should be accompanied by a unit test. That unit test should run automatically as part of your build pipeline.

Unit tests, properly written, weed out false assumptions and make your code easier to understand. If someone doesn’t know what a piece of code does, they can look at the unit test and see use cases. Writing tests can be a drag, and I don’t advocate for 100% test coverage, but if you ever go into a coding task thinking, _man, this one’s tricky_, that’s a sure sign that you should be writing tests along the way.

#### Conclusion

Good code is a joy to maintain, build upon, and solve problems with. Bad code is torture to the soul. Choose to write good code.

A good question to ask yourself when writing code is: will this be easy to delete when we don’t need it any more? If it’s deeply nested, copied-and-pasted all over the place, dependent on various levels of state and lines of code throughout the program, and otherwise craptastic, people will be unable to understand its purpose and impact and they’ll be uncomfortable deleting it. But if it’s immediately clear how it’s used and how many lines of code it interacts with, people will be able to delete it confidently when its usefulness runs out. I know you love your code, but the truth is that the world will be better off without it someday.

For a more complete discussion of what makes good code, I recommend the book _Code Complete_, by Steve McConnell. It’s a thick book (and a little dated) but it’s very readable and will help you grow from a “working code” programmer to a “good, clean, elegant code” programmer.
