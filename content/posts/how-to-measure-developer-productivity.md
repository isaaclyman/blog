---
title: "How to measure developer productivity"
categories: ["management"]
date: 2017-08-14T10:23:59-06:00
description: "Thoughts on a results-only environment"
draft: true
genre: "Technology"
tags: ["productivity", "agile"]
---

For this post, I anticipate a very skeptical audience--the common man's philosophy of management hasn't changed much since the Industrial Revolution, so what I'm about to say will be very uncomfortable for some managers and executives. To ease the pain, I'll be block-quoting imaginary objections that a manager might have, like this:

> Hi! I'm Marcos the middle manager, and I already don't like where this is going.

Don't worry, Marcos. Believe it or not, I'm on your side.

Down to business.

Everyone knows that it's dumb to judge a developer's productivity by the amount of code they write. That's like judging Congress by the number of bills they pass. It's just as bad to measure the number of commits a developer makes, the number of bugs they fix, or the number of features they write. Programming is a multidimensional activity, one with multiple inputs and outputs, and it resists this kind of simplification.

One of the problems with these metrics is that a metric is a request, and when you work with developers, you usually get _exactly_ what you ask for. If you ask for more lines of code, you will surely get them. And they will be the most awful lines of code you've ever seen. If you ask for more commits, you will get hundreds of them--hundreds of tiny, useless commits. If you ask for more bug fixes, you will get a constant influx of horrifically buggy features, each followed by a miles-long train of fixes. So please, don't ask for those things.

If you can believe it, there exists an even worse metric, and it's the one most companies use: the number of hours a developer spends in front of a computer screen. Unfortunately, there's no transitive property of development hours. One developer's 60 hour week may not be as productive as another developer's 20 hour week. In fact, a developer's 60 hour week may be less productive than _her own_ 20 hour week. Productivity is a fickle quality, and not all work possesses it in equal (or even positive) quantities. The 40 hour standard may work well in cigarette factories, but it's little more than an illusion when it comes to complex work.

> Marcos here. I think I see where this is going. You want to work 20 hours a week and get paid like a full-time employee, huh? Don't we all.

No, Marcos, not at all. I work hard. I usually do fine on a 40 hour week, assuming I get a few weeks of vacation each year. I'm not asking to work less hours. What I'm asking for is permission to be as productive as I can possibly be, whether that means working six hours or 60.

Perhaps you've heard the term _cargo cult_. It's a concept that extends the ["post hoc ergo propter hoc"](https://en.wikipedia.org/wiki/Post_hoc_ergo_propter_hoc) logical fallacy. The idea is: if you replicate the circumstances and behaviors surrounding a particular example of success, then you will achieve the same success. This fallacy is particularly annoying in the many articles that detail the morning routine, wardrobe, or diet of various CEOs and millionaires, with the implication that if you arise, dress, and eat like them, one day you will _be_ like them. This is patently false.

<sup>I think maybe everyone but me already knew what a cargo cult was. I first heard the phrase only a week or two ago, so I included a definition here.</sup>

The 40 hour work week is a cargo cult. In fact, _any_ time requirement for developers would be a cargo cult, partially because it assumes that "time in chair" correlates to "work produced," and partially because it doesn't actually measure the activities that are valuable to the company.

One possible source of friction between managers and developers is this: developers are trained to build things and be productive, and managers are trained to measure, analyze and improve processes. Managers subsist on a high-data diet. If they can measure something, they usually will. If they can't measure something, they will correlate it with something they can. This is good business sense in many cases, but here it can be problematic.

The trouble with the measure-and-improve approach is that managers risk choosing measurability over value, which makes the company poor and the developer unfulfilled.

To be clear: you, as a manager, cannot measure a developer's productivity on an individual level. Productivity in software development consists of multiple variables:

* How many features are produced.
* How much value these features provide.
* The scope and complexity of these features.
* The quality and consistency of the code being written.
* The quality of the unit tests accompanying the code.
* How quickly the code is written (all other things being equal, faster is indeed better. Of course, the other things are almost never equal).

You can easily measure the first one and the last one. You'll struggle to measure the others.

> Whoa there, I think I have a pretty good idea of how big or complex my product's features are.

Unfortunately, perceived complexity isn't a useful measurement. It's [almost impossible](https://xkcd.com/1425/) for a non-developer to understand the difference between what is "hard to code" and what is "easy to code".

> Hmm. Okay, but at least I know if the code is good, right? By how fast and bug-free the feature is?

No, not really. There's a correlation but it isn't particularly strong. The main metric of code quality is [how easy it is to read](/blog/posts/steps-to-better-code). Unless you can read code, you can't measure that.

Hold that thought for a moment, and let's look at the worst case scenario. Suppose a developer is not only lazy, but maliciously so. He intentionally implements every feature in the fastest, messiest way he can, only making enough effort to ensure that the feature isn't noticeably buggy or slow. He doesn't write unit tests, he doesn't account for edge cases, and he manages to navigate office politics in such a way that all the deceptively simple feature work gets assigned to him. You, dear manager, can measure him any way you like and you won't know he's underperforming.

But guess who will? His team.

This is where actual management skills come into play. A wise manager will speak with each member of the team on a regular basis and have enough trust and rapport with them that they will confide in him/her when they feel that a team member isn't pulling their weight. An effective manager will be able to detect when this information is accurate and when someone is just trying to undermine their teammate (hopefully this is rare). And an intuitive manager will be able to determine if the underperforming person is truly an underperformer (and needs to be let go) or is just in a bad headspace (and needs a pep talk and a vacation).

> Wait, you're saying I should reward temporary underperformers by telling them to take a break? That's not how management works.

It seems like a reversal of the [carrot-and-stick methodology](https://en.wikipedia.org/wiki/Carrot_and_stick), right? That's because developers aren't mules. Neither carrots nor sticks will motivate them. If you can imagine a mule that loves pulling carts, takes pride in his work, and is always trying to do a better job, that's a much better analogy. Development is immensely challenging and satisfying work, requiring the total devotion of one's brainpower, and any distraction--family problems, stress, boredom, depression--can significantly reduce one's capacity for it. Most developers are motivated to do their best work by the nature of the work itself. You don't need to push their buttons to get them to work hard. You may, however, need to make allowances for them to get into a decent mental state.
