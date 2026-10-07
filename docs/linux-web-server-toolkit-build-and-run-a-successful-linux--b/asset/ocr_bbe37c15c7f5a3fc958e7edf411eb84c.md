# Chapter 17

# Using Server APIs

FROM THE THINGS YOU'VE read in Chapters 10 and 16, you can see how much can be done using scripts on your Web server as they interact with forms that you create within your Web pages. But you can go even further than that when you use Application Programming Interfaces (APIs) for the Web server. Topics in this chapter include:

+   * The advantages of using APIs
* Examples of how APIs have been used
* An outline of the Netscape and Apache APIs
* How to use the APIs for your own projects

# What Are APIs?

You can probably do a lot with your Web server at this point. But I imagine you can also think of things you'd like to do with your Web server but can't see how to accomplish using the tools you've learned so far.

That's where web server Application Programming Interfaces, or APIs, come in. A set of APIs is like a set of programming functions that let you pass data back and forth between the Web server's core functionality and your added components.
APIs are developed to extend the capability of Web servers beyond what the designers of the server could immediately see. APIs allow you to add functionality that is more complex than standard Web server features, or just features that are more carefully suited to the needs of your site.

A server API allows you to interact at a much deeper level with the Web server. In fact, in both Apache and Netscape FastTrack, most of the functionality described in this book for these servers is implemented through the API. That means you have access to just about anything you need. API functions you add to the Web server function as rapidly as the Web server itself. While interpreted scripts and even C programs must be started as separate processes, loaded into memory, and initialized, a Web server module you create with one of the APIs is actually part of the Web server and therefore is loaded when the Web server starts and ready to work for you at any time.