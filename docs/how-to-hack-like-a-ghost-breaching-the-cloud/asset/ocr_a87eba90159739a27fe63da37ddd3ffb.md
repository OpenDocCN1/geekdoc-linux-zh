# How the Book Works

This is not your typical tech book. There won’t be tutorials, in the traditional sense. We take on the role of the hacker, and our target is the (fictional) political consultancy firm Gretsch Politico. I’ll walk you through a day (or several) in the life of a hacker, working from start to finish—from setting up a decent anonymous infrastructure, to performing some preliminary recon, to finally infiltrating and exploiting the target. The companies and names used herein are mostly fictional, with the exception of the obvious ones like Twitter and Kubernetes. So while there is plenty you can adapt and try out (and I encourage you to do so), you won’t be able to follow each step exactly as shown. For example, we’ll eventually hack the emails of the Gretsch Politico CEO, Alexandra Styx. Neither the company nor Styx herself exists.

As we feel out our journey, we’ll meet many dead ends and roadblocks, but I’ll show you how you can use even the most apparently meagre of results to set you on another path. This is how security works in the real world. Not every route will lead to success, but with enough perseverance, a tad of creativity and sheer luck, you can stumble upon some interesting findings.

To preserve our fourth wall, from now on we’ll speak of our targets as though they are as tangible as you or me.

Let’s talk about our target for this new hacking adventure. Gretsch Politico Consulting is a firm that helps future elected officials run their political campaigns. Gretsch Politico (which we’ll also refer to as GP) claims to have millions of data points and complex modeling profiles to effectively engage key audiences. As they nicely put it on their website, “Elections often come down to the last critical voters. Our data management and micro-targeting services help you reach the right people at the right time.”

In laymen’s terms: “We have a huge database of likes and dislikes of millions of people and can push whatever content is necessary to serve your political agenda.”

Much clearer but much scarier, right?

I wish I were making this stuff up, but sadly this whole charade is how almost every so-called democratic election works nowadays, so we might as well make it our training ground for this book’s hacking scenario.

# The Vague Plan

I don’t want to give too much away ahead of the game, but as a quick overview, the book is split into four parts. Part I, “Catch Me If You Can,” helps you set up a robust hacking infrastructure—one that guarantees online anonymity and resiliency. We’ll deck out an arsenal of custom scripts, containers, and Command and Control (C2) servers and build a backend attacking infrastructure in an automated fashion for maximum efficiency.

With our weapons in hand, Part II, “Try Harder,” lays out the basic recon you’ll need to perform in order to understand your targets as well as find those valuable vulnerabilities.