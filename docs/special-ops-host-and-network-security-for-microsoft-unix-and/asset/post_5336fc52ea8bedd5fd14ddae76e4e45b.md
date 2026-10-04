
# xxiv Foreword

Following this principle requires two things: first, the quality of the data collection is solid, and second, that your methods of analyzing that data are equally underestimated.

The first variable in collecting solid data, asset inventory, is one of the most underestimated of security. Understanding what assets exist, where they are located (for example, from what country, to what building, and in what room), and what criticality and value hold, is vitally important in calculating your security risk and can help you create a stellar security management program.

The second variable involves identifying vulnerabilities. The ability to derive an accurate vulnerability picture of your enterprise is critical to collecting baseline data. To do this, you must reduce false positives (reporting vulnerabilities present when there are actually none) and eliminate false negatives (not reporting a vulnerability when there are actually one).

The final variable is understanding the threats to your system. A vulnerability by itself is not a critical risk—only when a hacker takes a solid exploit, and begins using it it becomes a critical risk. To understand the nature of the threats relevant to you, you need to know the current activities of the underground, how they work and communicate, and how they eventually exploit known weaknesses. Without understanding your threats, your data (that is, your assets and vulnerabilities) do not exist in a context of security management.

Only when your data collection has enabled you to understand the threats to your system you can go about the task of securing it. This book provides you with the tools and techniques that can help you analyze your data and determine the fixes necessary to harden the "chewy inside" of your network according to Pareto's Principle. You will never be 100 percent secure from attackers, but you can be 100 percent if you are applying your resources to the battles that will matter most.

Data for its owns holds value. To provide a "complete picture of your risk." In actuality, those reports often provide little a confusing mix of irrelevant or conflicting concerns, combined with an avalanche of unqualified data. Without an effective, dynamic, robust interface to your data, and without acting upon Pareto's Principle, you may never shore up your true internal.

The definition of insanity is the same thing over and again while expecting a different result—so if you've been caught in the vicious cycle of generating too much unfiltered data, don't let the failures of the past go unheeded. Read this book, heed its warnings, and take steps to effectively manage your security today.

> —Stuart McClure, President & CTO Foundationstone, Inc.

> Co-Author, Hacking Exposed Fourth, Windows 2000, and Web Hacking Editions

![](img/729efc56f204a2ebffb8295c3a2dfdfb_24_0.png)

# Assessing Internal Network Security
by Erik Pace Birkholz

Solutions in this Chapter:

- Identifying Threats to Internal Network Security
- Internal Network Security Assessment Methodology
- Documenting Findings for Management
- Implementing Secure “Gold Standard” Baselines
- Summary
- Solutions Fast Track
- Frequently Asked Questions

# Introduction

As “techies,” we embrace the ability to understand the technology behind how and why things work, to a point beyond most other people’s interest. Usually what drives our interest is curiosity, a curiosity very similar to that which we experienced in childhood.

Curiosity comes in different shapes and sizes for children. I remember kids in my neighborhood wanting things like baseball gloves, model planes, or even chemistry sets. Each of these toys was a unique facilitator for the individual's curiosity. My curiosity began around fourth grade with my introduction to a Commodore Vic 20.

My best friend and I whipped through the pages of our “Introduction to BASIC” texts. First, we learned the fundamentals of BASIC, such as PRINT, IF, and GOTO. Before you know it, we were writing real programs. One summer we decided to use the “all-powerful” computing device to make our own Choose-Your-Own-Adventure book. Billy as it sounds now, those books were very cool to us.

The point is, BASIC allowed us to make our own version of a book. Computers enabled our creativity and curiosity. Eventually, the Commodore 64 came out and I was introduced to the concept of the modem (and the concept of getting yelled at making long-distance calls). Even though it was only 300 baud, the modem represented a new beginning for us; it was a connection to a new world of possibilities.

# Creating Opportunity for Curiosity and Mastery

Unfortunately, it’s all too common as adults that outside saturate us with tasks that drawn out our curiosity or keep us from bringing it to any productive level. Learning computer security is a bit of a conundrum in that way that if you want to become skilled, you need to feed your curiosity, but you can’t dedicate the time required because your job (even if it requires you to be skilled in security) could never allow the amount of time that following one’s curiosity demands.

This is important, to master a skill, whether your motivation is curiosity or something else, that motivation must also be accompanied by the ability to train intensively. (As computer scientist Jan L.A. van de Snipeschet quipped, “In theory, there is no difference between theory and practice. But, in practice, there is,”)

This is analogous to another love of mine, competing in Brazilian Jiu-Jitsu. It requires an enormous amount of dedication to train to master the art, but no

# Assessing Internal Network Security • Chapter 1

matter how much I love training, course on most days I must be at work instead of the gym. Given a reduction in projects and daily tasks, this many IT-centric types would spend more time training themselves in becoming skilled at defensive security and assessment techniques. This is an area that builds naturally on their preexisting motivations and interests. To be an expert in computer security requires a mastery of attack and defense. The theory is methodical and the skills are detail-oriented, but the application of it requires fluidity. You are constantly faced with very complex challenges, offering incredible latitude in its solution.

Based on my assertion, an outsider might think IT departments are bursting at the seams with IT militias, armed and ready to go forth and conquer the hosts and networks riddled with vulnerabilities. Alas, there are few militias, mostly employees hunting to fight the IT fires that threaten to take their jobs, rather than dealing with the unforeseen problems that might take it next. In my mind, this alludes to the reason why worms like Nimda, CodeRed, Spida, and Slapper are far dumb and hungry, thriving on a diet of host and network negligence. Since most networks are connected, the overall security risk of any given network is defined in part by the threats created by the vulnerabilities of others.

When they told us in college that the good could come from synergy, I doubted they host and network vulnerabilities in their model. Well, we have achieved synergy, but unfortunately the bad guys defined this equation. The overall network impact from each worm continues to be much greater than the sum of impact to each local host. The blame for this vulnerability-ridden nation does not rest in a single location, instead it is an amplification of a collective lack of opportunity given to people, process, policy, and technology.

# Where is the Cavalry?

Many executives see computer security (information security) as overhead. Until a security incident in their corporation reaches the news or affects the bottom line, they continue to see it that way. If you are one of the lucky ones that works with security-mined executives, you are exempt from this rant, but for the rest of you, this lack of effective support for information security creates a cause-and-effect situation.

Information security is usually a second job for already overworked IT departments. They are lashed to their duties of ensuring the availability of systems and other daily tasks and have little time to expand into areas that are not
