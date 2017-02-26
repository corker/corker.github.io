---
layout:     post
comments:   true
title:      "Notes on clean code"
subtitle:   "Not that the story need be long, but it will take a long while to make it short."
date:       2017-02-26 12:00:00
author:     "Michael Borisov"
header-img: "img/post-bg-01.jpg"
---

<p>
     It's often happen we say let the code do its job and I don't care how clean it is. Sometimes it's enough to get
     results out and move on. As an example when I scrape article titles and authors from a web site I don't care if
     somebody else or even myself need to read this code tomorrow. Although I often see code that has to last longer
     than one run in such a shape that some effort required to understand what it does. Sometimes I see such code and
     realize that it was me who was an author. How come? I was doing my best to produce clean and readable code for
     a sake of easy future changes. Let's see what would be my excuses for this obviously failure.
</p>
<p>
     First excuse I could think of is the lack of time. I had to finish my task and to move on. Usually it happens
     when I've spent some time already solving a puzzle but it turned out that the problem is more complex than I
     expected. I feel like I've spent too much time on this task already and I simply decide to wrap up without
     proper cleanup. How to avoid such situations in the future? I could create a task to finish the cleanup and
     do the task when I have time.
</p>
<p>
     Another one is my passion to code reuse and generalization. There is always a moment when code works well
     and it's time to make sure I have a clean solution. At this point I start cleaning up. This means I
     try to reduce noise to make sure the logic is clearly visible and everybody can read it almost like English text.
     Sometimes I find myself so deep in the refactoring process that I went too far away and instead of one function
     I have three interfaces and ten little functions that nobody could match together without additional effort
     connecting these tiny pieces. How to avoid such situations in the future? I could ask my colleague to
     take a look if he could understand it quickly. We all aware of user testing. Here is the same idea.
</p>
<p>
     Well, what else. At this moment it's become tricky. I don't easily give up on code style moving from one
     programming language to another. Ones I found myself using C++ coding guidelines for C# with all the nice
     "m_" notations that have so much sense when write code in C++. My C# style looked similar to my C++, although
     there was no reason for it. Later I've realized how much noise actually I've introduced. I'd never do this
     mistake again. I carefully examine code style guidelines for every language I use and try to understand what
     are the reasons behind those rules.
</p>
<p>
     There is another situation I could think of. When first solution has been implemented and I have to extend it
     with a new requirement. There is always a chance that idea behind the original solution doesn't fit into the new
     situation. I often found myself limited with original abstract without challenging it. Result of this mistake
     could be two abstracts stuffed in one solution. One solution per abstract is easier to maintain. How to avoid
     such situations? When I struggle to find a good solution within a current implementation I could get back to the
     drawing board to make sure I clearly understand both abstractions.
</p>
<p>
     The last one I want to mention here is performance optimization. I know how important to have a good performance
     for my solutions. Although I found out that in most of the cases my premature optimizations only take time and
     make code less readable and I've had to do performance optimization again when I've been done with functionality.
     How to avoid such situations? Focus on functionality first, then do performance optimization when really needed.
</p>
<p>
     I like clean code. It's the same as keeping my table clean helps to clean my mind. I could better understand
     a problem I work on. I could find a better solution. I could introduce less bugs. Bugs are hiding behind our
     blind spots. You could say I don't care as long as my solution produce good results. Well, that is your choice.
     I like to live in clean environment. My code is a part of my living space. I spend days working with it.
     Of course there are places I don't visit often and I don't care so much how dusty is it. But in general I like
     to live in a clean environment.
</p>
<p>
     Happy coding,<br/>
     Michael Borisov.
</p>
