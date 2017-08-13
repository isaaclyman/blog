---
title: "Developer-driven development"
categories: ["development"]
date: 2016-11-06T04:59:40.751Z
description: "How we code at DirectScale, Inc."
draft: false
genre: "Technology"
tags: ["agile", "software construction"]
---

The company I work for is slowly losing its "startup" status. I’m trying not to be too nostalgic about it. After all, it means we’re doing well; a slew of truly impressive awards and contracts in recent months means we’re doing *great*. There’s a lot to be grateful for. At the same time, a lot is changing.

As this transition has played out, we’ve had to upgrade a few things. We’ve hired a CTO and an Enterprise Architect. Phrases like "PCI compliance", "load testing" and "root cause analysis" are becoming standard fare in the office. We’re becoming more cautious about deploying production code. We’re growing up.

But a lot of things have stayed the same — we’re still the same company where it counts. When I arrived, I learned that the fight against technical debt was a high priority around here; it still is. Our counterculture attitude toward code reviews is still going strong. We still wear a lot of hats. We’re moving quickly, so we can only keep what works — some practices are being proven and others are being discarded. And thanks to the foresight of our early hires, there’s more of the former than the latter. Our development workflow has been the same for as long as I’ve been around. It works really well.

I’ll go beyond that, though. We don’t keep doing things the same way just because it works. Practically anything *works* if you have unlimited time and funds and a few hardworking developers. *Works* is incidental. What matters more to me is that our process makes my Type-A, obsessive, engineer-personality heart feel good. We don’t waste a lot of time, our code base doesn’t get worse over time, I don’t have to build features I hate, and our workflow doesn’t frustrate me on a daily basis. If you’re a software engineer you must understand how good that sounds.

Our secret ingredient, I’ve decided, is something like this:

{{< tweet 793853934544781312 >}}

We do the second one.

People in general (*including* developers) have a tendency to treat developers like code-writing machines, brainiacs who wear headphones and crank out `switch` statements. But this stereotype falls short of our full potential — otherwise, a developer’s value would be determined solely by her technical knowledge and typing speed. A developer at her best is a Swiss Army Knife for software — someone whose creative, insightful and rational thought process makes her a valuable part of any discussion in the company. Companies that appreciate this fact have happier, more productive developers — developers who (believe it or not) don’t spend 100% of their time staring at code. DirectScale excels at this.

So enough hype: what exactly are we doing, and why am I convinced that it represents a set of common-sense best practices — not just for us, but for any software team? That’s a question that merits a multi-part answer. Let’s dive in.

## What we don’t do (ever)

An average "Agile" workflow at an average company goes like this:

1. Someone in a dark gray suit decides that a new feature should be built.
1. He gathers with two other executives and blithely decides what the feature should do and what it should look like. No one’s consulted a developer yet (more on this later) so the whole idea is hopelessly naive.
1. They pack up their conversation and send an email to the highest-ranking non-developer in the Code Zoo. They leave out a few important details.
1. The non-developer (a project manager? A product owner? A scrum master? Insert the latest trend) writes up a set of business requirements based partially on the email, partially on her conception of the company’s mission, and partially on personal druthers. Over the next two days, these business requirements are mystically transformed into a set of user stories.
1. A developer is assigned one of the user stories. If he’s extremely unlucky, he has to estimate how long it’s going to take him to finish; this involves both advanced calculus and a particular form of voodoo. He immediately starts thinking in code and has written 55 lines of pristine, elegant C♯ before he can stop himself. The connection between brain and keyboard is like Niagara Falls. The feature comes to life suddenly. He submits a pull request and kisses his fingertips like a French chef.
1. The developer’s team lead reviews the pull request and rejects it with 17 explanatory comments: this code is not performant, this method doesn’t cover an edge case, that class reads like a horror novel, and the resultant feature doesn’t look anything like the original specification.
1. The developer rewrites his code twice with plenty of back-and-forth from the team lead. Two days later they’re both satisfied with the result.
1. The code is merged and deployed to production the same day.
1. A few days later the executives read a brand-new set of release notes, very pleased with everything that happened during the sprint. One of them wonders why the feature he requested wasn’t built. He begins again at step 2.

This obviously isn’t great. It’s the love-child of [Chinese Whispers](https://en.wikipedia.org/wiki/Chinese_whispers), Pictionary and 20 Questions, which may be great games but are not great ways to run a company. All the same, silicon’s best and brightest stand by it, it’s peddled by Agile coaches, and it’s the default methodology for young teams.

We can do better, starting from the very first step.

## Developer involvement and buy-in

At DirectScale, we don’t hire a bunch of Idea People to sit around and imagine up cool things for us to build. I hate to break it to you, but "Idea Person" isn’t a real job. Sorry. The fact is, *everyone* has ideas. Everyone can offer good suggestions for how your product can improve and what problems it can solve. Companies, in return, can encourage those ideas or they can repress them. Most companies choose to repress, albeit in subtle ways — leaving developers and designers out of product vision discussions, passing instructions and requests through a middleman, or writing off developer push-back as "laziness" and "complaining."

A better method is to make sure a representative from each phase of the development process is present in every meeting about every feature, from inception to completion. Instead of waiting until the next sprint to find out that your feature isn’t technically feasible, why not find out right now? Yes, this means your developers are spending a lot of time AFK (away from keyboard). But if you invite their feedback and listen to them, it also means that they’ll buy in — they’ll commit to the shared vision of the team and take ownership of the feature, which will mean faster and better turnaround on their part. For bigger features, you need more buy-in, which means more developers in the room.

As I mentioned, this also prevents you from wasting several days dreaming up a feature that the developers can’t (or shouldn’t) build. As most of us have learned, features that seem straightforward can sometimes be incredibly complex, impossible or illegal. Nobody likes to find this out after the feature’s release date has already been scheduled.

The most recent meeting I was in was a [Design Studio](https://www.targetprocess.com/blog/2011/05/ux-meets-agile-design-studio-methodology/) for a large feature set which may come to represent DirectScale’s single largest source of income in future years. It’s the most important product vertical we’ve discussed all year. Guess who attended?

* A UX designer
* Three or four developers
* A graphic designer
* Our project manager

The functionality we were going to build had not been described in great detail by the higher-ups and not a single C-Something-O or VP was present. It was all us. And why not? We had come prepared; our UX designer and project manager both have industry experience and they had interviewed several customers who might use the feature set. The executive team had expressed their expectations (without trying to control the creative process). We’d already had a few discussions in which we had defined the scope of the problem to be solved. And we were the ones who were going to build the thing, after all.

Two and a half hours later (a longer meeting than usual, but worth it), we emerged with some sketches and a shared understanding of the first piece of the puzzle, each of us satisfied that our ideas had been a part of the result. That’s how our product comes to life.

## Dev designs (code reviews in reverse)

Once our ideas have metamorphosed into a prototype, we get ready to code. But we don’t open our IDE’s just yet.

See, software construction is a lost art. Steve McConnell, author of *Code Complete*, spends a couple of impassioned chapters talking about the space between the creation of business requirements and the writing of code — the space when, according to him, the brightest architects in the office should be drawing detailed maps of every class, interface, interaction and data point that’s about to be written. From McConnell’s perspective, writing code with nothing but a user story or a design is like building a skyscraper without a blueprint.

But somehow, [most companies have forgotten](http://dilbert.com/strip/2007-11-26) how to plan.

The problem is between steps 4 and 5 in our example Agile process. After the user stories were defined but before the developer started tickling the keyboard — what happened? In most cases, nothing.

An experienced developer may be able to foresee all the work needed for simple tasks. But even the best of us run into unforeseen obstacles. We’ve all had that oh-crap moment when, just as we’re writing one final line of code, we realize that an entire set of situations isn’t accounted for in our logic.

Then there’s the sinking feeling of discovering that a new member of the team has written an entire class to solve a problem that already has a standard, reusable solution elsewhere in the code. Five minutes of knowledge-sharing before coding began would have prevented three hours of reinventing the wheel.

When code isn’t planned out *as code*, none of our well-intentioned processes can succeed: standards are ignored, reusability dies out, and code becomes more scattered and bug-ridden over time. Inside of a few short years, you’re dealing with legacy code (shudder). Certain issues will come out in the code review, but by then so much has gone to waste: hours of development time, several problem-solving cycles, and the developer’s enthusiasm and dedication.

All of these problems could be avoided (or at least mitigated) by exactly the thing Steve McConnell recommended in 1993: planning ahead.

At DirectScale, we’ve turned the code review on its head. Instead of reviewing code after the fact, we make sure it’s correct ahead of time. We plan ahead. We call this the Dev Design, and it looks a lot like a collaborative code review performed before anyone has written a single line of code. It works like this:

1. A user story is created.
1. A developer is assigned to design the work required for the story.
1. The developer looks at the requirements, digs through the codebase for anything useful or relevant, researches the libraries and techniques that may be needed, and writes out a detailed, step-by-step description of how he would write the code needed to complete the user story. The resulting document (the Dev Design) includes all the variable names, caching techniques, classes, interfaces, and interactions that will end up in the code. In tricky cases, the developer may even include several lines of pseudocode.
1. The developer schedules a meeting with the other developers on his team. Together they review the Dev Design and alter it as needed, suggesting alternative methods, sharing knowledge, and making architectural decisions.
1. The team completes the tasks as specified in the Dev Design. If there’s a problem that forces them to diverge from it, they discuss it on the spot and decide what to do.
1. Most of the time, no code review is required. The code is merged and submitted for QA as-is.

The amount of back-and-forth we avoid by doing things this way really is phenomenal. At a previous company, under an especially finicky team lead, I averaged almost five rewrites per pull request. Now I average zero. Planning ahead ensures that things get done the right way, the first time.

## 20% time (not [the Google kind](https://googleblog.blogspot.com/2006/05/googles-20-percent-time-in-action.html))

At DirectScale we don’t allow technical debt to pile up. As technical debt gets older, it grows (just like regular debt) and when it reaches critical mass, it invariably ends up breaking the user experience and annoying clients. What’s worse, it frustrates coders and can cause serious instances of the "[what-the-hell effect](https://www.theguardian.com/lifeandstyle/2014/may/24/this-column-change-life-what-the-hell-effect)" for anyone who has to work with the affected code.

Resolving technical debt, though, is a counter-intuitive activity. For starters, it doesn’t look like anything. If a senior developer spends a week paying off technical debt — refactoring code, splitting classes, smoothing out kludges, accounting for edge cases — what does he have to show for it? Other developers will appreciate the difference, but anyone with the word "manager" in their job title is forced to go on faith. Nothing new can be shown to clients, no urgent bugs have been fixed, the application may not even be noticeably faster. If a product owner finds the line "addressed technical debt" in your release notes, how do they know you weren’t playing flick-the-paper-football all week? They don’t.
But the "debt" analogy holds true for this situation. Say you’re in $15,000 of credit card debt. If you spend your next three paychecks paying it down, what do you have to show for it? Really not much — no new furniture, no fancy dinners, no repairs for your furnace or car. But you are *much better off* than you were. And you better know it.

To prevent both managers and developers from getting too caught up in deadlines and features to invest in healthy code, we enforce a strict minimum: at least 20% of our time is spent fighting technical debt. That means one in every five user stories. A few times a week, we’re standardizing, refactoring, load testing, researching, creating developer resources. We’re doing things that our clients will never know about. But what they do know is that our software is more cutting-edge, reliable and delightful than anything they’ve ever used. And they aren’t afraid to say so.

Although the work we do to address technical debt isn’t always exciting (refactoring, in particular, is one of the most challenging and tedious things a developer does) and although it doesn’t provide the instant gratification that feature-driven tasks do, it is rewarding. The feeling of tweaking and improving pure code for a day or two is something like the feeling of recovering from a cold: the world just seems brighter afterward. You look back and see that your code is sensible and maintainable in a way it wasn’t before — it looks like something out of a textbook. And your work pays off for months to come. Working with code that has been properly cared for is a constant relief.

## Story despecialization

Startups are infamous for requiring their employees to wear a lot of different hats. Some companies treat job titles as an afterthought; at various times you may end up being (as I have been) a back-end developer, a front-end developer, a QA engineer, a technical writer, a Spanish translator, a usability interviewer, and a printer support technician. Some people dislike this characteristic of small companies. I love it.

On our team we encourage despecialization all the way down to individual user stories. In some companies this is called "swarming." Our method goes like this: when a developer is ready for another task, he is assigned the topmost task on our priority board whether or not he worked on the other tasks in the user story (and whether or not he knows how to do it). Our team is responsible for a product, not a programming language — if you knew T-SQL, C#, .NET, JavaScript, Angular.JS and SASS when we hired you, that’s great. If not, you’ll learn as you complete the tasks that require them. This makes us more like artisans than assembly line workers. Our goal is to make sure that every one of us knows enough about every part of the source code to work with it effectively, especially in an urgent situation.

This also ensures that our team passes the "[bus test](https://medium.nobl.io/the-bus-test-2338d474b193#.xi6oujm7c)": if a random member of our team were hit by a bus tomorrow, would we be able to continue without a hitch? Or would someone have to be assigned the uphill task of figuring out how to maintain the code that was under their jurisdiction? The bus test is especially telling at DirectScale, where I’m surrounded by highly talented and competent coworkers, people who are passionate about subjects I’m barely conversant in. But I like to think we’d pass it. Even if our most intelligent and hardworking employee were to die suddenly, the work would go forward. And no one would even miss me that much (I kid, I kid).

## Brown bags and professional development

DirectScale encourages a culture of constant learning and improving. This goes beyond sponsored PluralSight memberships or a company library. We recognize that the best teachers are the ones who work among us and the best classroom is the one where personal interactions and discussions are the lesson plan. To that end, we take time once or twice a month to learn from each other in a group setting. We call this a [brown bag](http://www.investopedia.com/terms/b/brown-bag-meeting.asp).

This usually entails a presentation from someone in the company who knows more about a certain technology or skill than the rest of us. We’ve had brown bags about topics as diverse as CSS, teamwork, sleeping habits, and SQL debugging. Anything is fair game.

Like despecialization, this helps us to pass the bus test. The amount of information a truly passionate person can communicate in an informal one-hour meeting is impressive.

It also improves developer happiness. [Developers are happiest when they are learning and growing](http://www.softwarebyrob.com/2006/10/31/nine-things-developers-want-more-than-money/). My best days at work — the days when I come home beaming, totally jazzed about my job — have been the days that I learned a new framework or concept and started putting it to good use. We developers get a huge thrill out of learning new things.

## Why so happy?

I’ve spent a lot of time detailing the things that make me happy at work. And although I’ve tried to balance this by pointing out all the other benefits of our workplace methods and philosophies, I’m a little worried that someone will read this and totally miss the point. At some company, somewhere — a company that too many of my developer friends seem to have worked for — there is a group of middle managers who are stuck in the year 1906 and all they can think is "Who cares if you’re happy?" To them, developers are like dairy cows. You lock them in a cage, you milk them for as many lines of code as they’re willing to produce, and then you get rid of them. If one quits, another will take his place, so long as the salary is appealing enough.

If you ever have the misfortune of managing someone with this attitude, I invite you to fire them.

Here’s a news flash: [happy](http://www.itworld.com/article/2693429/big-data/study-proves-that-happy-programmers-are-better-programmers.html) [developers](https://devzone.zend.com/5473/happy-developers-productive-developers/) [do](https://www.entrepreneur.com/article/249528) [incredible](http://techbeacon.com/lessons-agile-happier-teams-are-more-productive-so-spread-cheer) [work](http://www.sandeepmvp.com/developer-hapiness/). In fact, this is almost a foregone conclusion — the question successful companies are asking isn’t "Should we treat our developers well?" It’s "How can we make our developers happier?"

On the flip side, unhappy developers produce poor code for a little while and then quit. If you don’t treat developer happiness as a company-wide priority, you will eventually be forced to treat [developer turnover as a company-wide crisis](http://www.developerdotstar.com/mag/articles/software_team_turnover.html).

I realize that as a developer it’s in my own best interest to say this. You could accuse me of being a diva. And maybe you’re right. But if I’m a diva, I’m a diva that bleeds excellent software from all ten fingertips. Right now the demand for divas like me [is](https://itif.org/publications/2016/05/31/us-must-expand-computer-science-education-keep-demand-skilled-workforce-itif) [through](http://www.seattletimes.com/seattle-news/education/with-surge-in-computer-science-majors-state-colleges-struggle-to-keep-pace/) [the](http://www.geekwire.com/2014/analysis-examining-computer-science-education-explosion/) [roof](http://www.bls.gov/ooh/computer-and-information-technology/software-developers.htm). And I’m far from being the best or the brightest in my field.

To put it simply, there are *no* benefits to trying to optimize developers the way you would optimize an assembly line at a cigarette factory. You have to let them do things their way. But you’ll be pleased with the results. Happy developers write good code. And developers who write good code are happy.

## Conclusion

I’ve given you just a peek at what it’s like to work for [a company that really understands software development](http://directscale.com/). I wish you could see the full panorama. I haven’t been a programmer for very long, all things considered, but it’s changed my entire outlook on the industry.

As you’re probably aware, developers are the target of [intense recruitment techniques](https://medium.com/@isaaclyman/how-to-recruit-me-e82580ae91f1). I hear from recruiters regularly, and one of them even talked me into a lunch date a few months ago. I made sure to ask him a few simple questions:

* To what extent are developers involved in your design and discovery process?
* How do you address technical debt?
* How do code reviews go at your company?
* How much "bad code" would you say there is in your codebase?

This made him uncomfortable. But (to his credit) he was honest with me: these weren’t high priorities at his company. I thanked him for lunch and let him know I wasn’t interested in any further conversations.

Listen: if you still think that foosball and Coke make developers happy, I’m here to tell you they don’t. Sure, perks like that are nice. But what makes us developers really happy is solving challenges every day and building code that’s familiar, well-written and full of features we’re proud of.

If you can’t offer us that, you really don’t have much to offer.
