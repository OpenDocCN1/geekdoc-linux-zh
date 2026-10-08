# THE METHODOLOGY OF WEB HACKING

The central goal of this book is to set forth a Web application security review methodology that is comprehensive, approachable, and repeatable by readers who wish to apply the wisdom weve gained over years of performing them professionally. The basic steps in the methodology are

+   * Profile the infrastructure
* Attack Web servers
* Survey the application
* Attack the authentication mechanism
* Attack the authorization schemes
* Perform a functional analysis
* Exploit the data connectivity
* Attack the management interfaces
* Attack the client
* Launch a denial-of-service attack

This book is structured around each of these steps—we dedicated a chapter to each step so that by the end of your read, you should have a clear idea of how to find and fix the most severe security vulnerabilities in your own site. The following sections will offer a brief preview of what is to come.

# Profile the Infrastructure

The first step in the methodology is to glean a high-level understanding of the target Web infrastructure. Each component of Figure 1-1 should be reviewed: Is there a special client necessary to connect to the application? What transports does it use? Over which ports? How many servers are there? Is there a load balancer? What is the make and model of the Web server(s)? External sites are relied on for some functionality? Chapter 2 will discuss the tools and techniques for answering these questions and more.

# Attack Web Servers

The sheer number of Web server vulnerabilities that have been published makes this one of the first and usually most fruitful areas of research for a Web hacker. If site administration is sloppy, you might hit the jackpot here—Chapter 3 will describe several attacks that yield remote superuser control over a Web server, all over TCP port 80.

# Survey the Application

If no serious vulnerabilities have been found, good for the application designers (or maybe they’re just lucky). Now attention turns to a more granular examination of the