---
layout:      post
title:       "On Documentation"
date:        2015-06-14 12:18
description: My take on why programmers should document their code and how to do it.
tags:        programming, documentation, engineering
---
I'm a big fan of documenting my code and it's a surefire headache for me when I work in a legacy system lacking useful documentation. I haven't decided if I hate absent, useless, or inaccurate documentation more but they each present their own problems.

I try to avoid take extreme or absolute stances on things, though, so I'll take some time to cover when it's appropriate to not document code. Make no mistake, even an ardent supporter of documentation like me can see the benefits of breaking with my default mode.

##So...What Is It?##
"Documentation" is a pretty broad category in my experience. Software engineers will generally write two kinds: comments and technical specifications. I also believe a robust test suite falls under this umbrella.

It's also important to remember requirements specifications, technical manuals, cookbooks, white papers, and probably many more things I just can't think of right now. I've contributed in some way to most of these, too, and they all have their place.

#Comments: a Hate/Love Relationship#
The most frequent and worst argument against writing comments is that it's time consuming or some other phrase which boils down to people being lazy. The obvious problem with this is that any job should be done well and thoroughly. If it's appropriate to write comments, the _what_ and _how_ will be obvious to the author.

The problem, then, is deciding if it _is_ appropriate. Properly object oriented code will avoid god methods, vague naming conventions, and a lack of domain-specific grammar. If that's all true, then method names will clearly communicate what consumers can expect and implementations will be concise. Code in that condition will only be polluted by comments, except for one very specific case: API documentation.

On the plus side, this lives in a block preceding the method so it doesn't break up the flow of code and it can (usually) be collapsed for those who don't want to see it in their files. It makes for a nice compromise between people in both camps.

The real benefit to this is the tools that turn the comments into websites. Well-documented languages like Java and Ruby have fantastic sites showing the ins and outs of the API.

#What About In-Line Comments?#
In an ideal world, these aren't needed nor used since they disrupt the narrative the code itself should tell. In my OpenInteger gem, I've had the benefit of being the only person working on it so I've been able to make my largest method only eight lines and I haven't seen a reason to write in-line comments.

Most of the time, though, I don't live in that ideal world. I work on legacy systems with god methods, terribly-named variables (lots of `x` and even `obj`), and blocks of declarations, loops inside of loops inside of loops, and other nightmare situations. I work under deadlines in environments where I'm encouraged to cut out luxuries like cleaner implementations and object orientation.

In that world, I absolutely _need_ in-line comments. I need to write them and I need others to write them. Without signposts like that, I've spent hours hounding the original authors for details which, obviously, they can't remember because they wrote that five years ago in a day-long rage-filled haze of firefighting. That person, then, ends up taking time to figure stuff out with me so now twice as many man-hours are burning.

Even worse than that are the times that the author and everyone associated with that system have left the company. This is code that exists in a wasteland. Nobody has touched it in years. The higher-ups are afraid of it. Those of us on the front lines dream of burning it down and starting over. These places are documented with illustrations of dragons. The tacit understanding is that here there be monsters. Abandon hope all ye who enter.

All because the authors didn't or weren't given the freedom to do their jobs properly.

#Technical Specifications: Or Essays For Nerds#
These are behemoths far overshadowing comments. These are dissertations which take a set of seemingly innocent high-level expectations and translate them into more down-and-dirty language that presents a unified front about the implementation and maintainability strategies.

There are two major reasons to write these: they map out the expected course for the features or updates at hand and they provide references for future engineers. They outline the intentions for the system at large which can be invaluable for people maintaining and extending it later on.

The trick is that these take much greater attention to detail and a willingness to analyze current systems and make certain assumptions. Beyond all that, everyone involved needs to understand Dwight D. Eisenhower: "...plans are useless, but planning is indispensable."

Writing designs forces to you develop insights into the systems and learn how to communicate ideas about them. Designing the software rather than just tacking code on ad-hoc is the difference between being the only guy with at least some experiene in the system and the expert in it. It's the difference between forcing future engineers to guess and building something teachable.

So, when is it appropriate to not write a specification? There's a fuzzy middle ground but certain things fall into clearly defined sides. Any feature set requires at least a little love, even if it's just a few pages.

It makes more sense to document a single bug in the bug report, though.A lonely atomic enhancement can also be documented in a work item.

If you can create a set of bugs and enhancements, though, you'll benefit from writing a spec. Ultimately, it takes a critical mind to decide when it's appropriate and just a little pride in your work to actually do it.

#Conclusion#
These aren't hard and fast rules, just the observations I've been lead to by my years in the industry. I appreciate teaching and learning and I intend to never become one of those engineers whose successors cringe when code has my name attached.

Ultimately, don't ever assume you'll always understand what you did at the time and take it for granted that other people down the line will need to know what the hell you were thinking.
