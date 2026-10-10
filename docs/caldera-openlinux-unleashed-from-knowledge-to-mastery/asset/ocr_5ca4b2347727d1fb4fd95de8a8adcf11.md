passing it through to the client as it appears in the HTML.

Using the first pytexit method, where we are generating static pages, all processing is done once on the *server side*. This is similar to a C program that is compiled once and the resultant executable is executed many times. The resultant pages are then transmitted directly to the client. For each hit, no pytexit processing occurs at all. The Web server simply transmits text files that were generated earlier.

When using pytxt to create dynamic content by using #!/usr/local/bin/pytxt scripts, all processing is done on the server side, and the page is dynamically regenerated for every page hit. In this case, the Web server is actually executing pytxt to generate the Web page, and the output is sent back to the client. We hope this helps you to understand various uses of pytxt.

With the pytxt command and a bit of creativity, you can easily automatically generate your own Web page or an entire Web site. You are now encouraged to engage your mind and become the next Internet millionaire!

# Object-Oriented Programming

At its heart, Python is an object-oriented language, and by this point, you have used many of Python's object-oriented features in our programs, maybe without your even knowing it. Previously, we have only interacted with the standard objects that Python provides, but now we're going to learn how to create our own objects that are customized to our specific needs. We've worked with Python objects before, but now it's time to learn how to make Python objects work for us.

# Intro to OOP—How to Not Get Confused

The biggest mistake you can make in trying to understand object-oriented programming (OOP) is to buy into all of the hype that circulates regarding this technology, calling OOP such things as "the next programming paradigm" and "the wave of the future." Forget it all and remember one thing—although OOP comes with its own terminology and syntax, it is primarily an organizational method designed to make life easier for you, the programmer. It's not some magic formula for "incredible code."

OOP is very good at addressing programming problems that are organizational in nature. It allows you to group functions and related data together into an object, providing a clearer and more compact syntax for our programs. For example, if we have a bunch of functions that operate on a special data structure called a "glorp," it would not be unusual for them to have names like:

...