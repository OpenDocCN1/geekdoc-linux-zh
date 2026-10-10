application on a slow system that is becoming increasingly costly to maintain.

The payoff in using text comes when you must port your application to a new architecture. If you had enough foresight to make your program portable, then with text it becomes a trivial matter to move your data to a new platform as well. Woe to software engineers who must port both data and program code. The data will be stale by the time it ever sees the new memory boards. The cumulative time lost by a 3:1 performance reduction pales in comparison with the weeks or months lost in moving the data to the new platform.

# ### 4.2.5 The lack of speed is overcome by next year's machine

We've acknowledged that text files impose a drag on performance. You could possibly realize up to a 3:1 reduction in speed. However, if the application meets today's minimum performance requirements, you can expect that next year's machine will yield a dramatic improvement— if your data can be ported.

As of this writing, next year's machine usually offers enough additional computing power to render any of today's performance concerns about text files superfluous. In other words, if your application barely performs adequately today, its speed will be ample tomorrow. In a few years you may even have to start thinking about how to slow it down so people can use it!

# **Case Study: One Unix Philosopher's Bag Of Tricks**

We have seen that given a choice between high efficiency and high portability, Unix programmers' preference weighs heavily with the latter. As a result, their applications are often among the first to run on new platforms as they become available. This gives their software a definite edge in the marketplace. In a world where windows of opportunity open overnight and slam shut as soon as a month later, pursuing the portability priority can mean the difference between being an industry leader or being one of the others that wish they were.

How did Unix programmers come to embrace such beliefs? Most early software engineers weren't taught the importance of portability in school, at least not with any sense of conviction. More likely, they learned the value of portable code and data the best way: through firsthand experience.

Most Unix "gurus," as they're called, carry a collection of programs and shell scripts that make up their personal tool kit. These tools have followed them as they've moved from machine to machine, job to job, and company to company. For purposes of illustration, let's look at a Unix philosopher's bag of tricks.

My personal collection of tools has varied through the years. Here is a partial sample of those that have stood the tests of time and portability:

cal | A shell script front end to the Unix cal program that allows you to specify textual names for months instead of numbers. Borrowed from *The Unix Programming Environment* by Brian Kernighan and Rob Pike. [a]