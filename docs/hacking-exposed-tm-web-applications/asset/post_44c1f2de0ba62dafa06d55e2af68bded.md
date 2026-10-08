
# Hacking Exposed Web Applications

![](img/2c61c2d28445b774d9266972920f432d_44_0.png)

**Figure 1-4.** A typical load balancing setup; note that Client A's connection is routed to server www1, while Clients B and C are routed to server www3 based on the load balancer's algorithm

# The Model: Web Services

As we've noted more than once in this chapter, the Web is constantly evolving. What's in store for Web application architectures in the near future? As we write this, the words on everybody's lips are *Web services*.

Looking at Figure 1-1 again, Web services are comparable to self-contained, modular Web applications. Web services are based on a set of much-used Internet standards-development. These standards include the Web Services Definition Language (WSDL), XML format for describing network services; the Universal Description, Discovery, and Integration (UDDI) specification, a set of XML protocols and an infrastructure for the description and discovery of Web services; and the Simple Object Access Protocol (SOAP), an XML-based protocol for messaging and RPC-style communication between Web services. (Is anyone not convinced XML will play an important role in the future of the Web?) Leveraging these three technologies, Web services can be mixed and matched to create innovative applications, processes, and value chains.

A quick review of this chapter will tell you how Web services are being held out as the Holy Grail for Web developers. As shown in Table 1-1, there are several competing standards for information interchange between Web applications today. Thus, integrating

# Chapter 1: Introduction to Web Applications and Security

two or more Web applications is generally an arduous task of coordinating standards to pass data, protocols, platforms, and so on.

Web services alleviate a lot of work because they can describe their functionality and interact dynamically with other Web services via WSDL, UDDI, and SOAP. Web services provide a means for different organizations to connect their applications with one another to dynamic e-business across a network, no matter what their application, design, or run-time environment (ASP, ISAPI, COM, J2EE, CORBA, and so on).

WSDL, UDDI and SOAP grew out of collaborative efforts between Microsoft and various other vendors (including IBM, Ariba, Developer, and UserLand). Many of the large technologies move like Sun and Oracle are also on the Web service bandwagon, even when the current standards may not look the same in six months, it's clear that Web services are here for the long haul. And of course, there will be a whole new near of security woes as these new technologies move from crawling to walking. We'll look at what's in store security-wise in Chapter 10.

# POTENTIAL WEAK SPOTS

Now that we've described a typical Web application architecture, let's delve into the topics that we will cover in more detail in the coming chapters. Namely, what are the commonly exploited weaknesses in the model we have just described?

Once again referring to Figure 1-1, what components of our stereotypical Web application architecture would you the most vulnerable to attack? If you guessed “all of them,” then you are familiar with the concept of the trick question, and you are also correct. Here is a quick overview of the types of attacks that are typically made against each component of the architecture presented in Figure 1-1.

- ▼ Client Active content execution, client software vulnerability exploitation, cross-site scripting errors. Web client hacking is discussed in Chapter 12.
- ▶ Eavesdropping on client-server communications, SSL redirection.
- ■ Web Server software vulnerabilities. See Chapter 3.
- ■ Application Attacks against authentication, authorization, site structure, input validation, and application logic. Covered in the rest of this book.
- ▲ Database Running privileged commands via database queries, query manipulation to extract excessive datasets. Tackled in Chapter 9.

Now that we've defined the target, let's discuss the approach we'll take for identifying and exploiting these vulnerabilities.

# THE METHODOLOGY OF WEB HACKING

The central goal of this book is to set forth a Web application security review methodology that is comprehensive, approachable, and repeatable by readers who wish to apply the wisdom we've gained over years of performing them professionally. The basic steps in the methodology are

- Profile the infrastructure
- Attack Web servers
- Survey the application
- Attack the authentication mechanism
- Attack the authorization schemes
- Perform a functional analysis
- Exploit the data connectivity
- Attack the management interfaces
- Attack the client
- Launch a denial-of-service attack

This book is structured around each of these steps—we dedicated a chapter to each step so that by the end of your read, you should have a clear idea of how to find and fix the most severe security vulnerabilities in your own site. The following sections will offer a brief preview of what is to come.

# Profile the Infrastructure

The first step in the methodology is to glean a high-level understanding of the target Web infrastructure. Each component of Figure 1-1 should be reviewed: Is there a special client necessary to connect to the application? What transports does it use? Over which ports? How many servers are there? Is there a load balancer? What is the make and model of the Web server(s)? External sites are relied on for some functionality? Chapter 2 will discuss the tools and techniques for answering these questions and more.

# Attack Web Servers

The sheer number of Web server vulnerabilities that have been published makes this one of the first and usually most fruitful areas of research for a Web hacker. If site administration is sloppy, you might hit the jackpot here—Chapter 3 will describe several attacks that yield remote superuser control over a Web server, all over TCP port 80.

# Survey the Application

If no serious vulnerabilities have been found, good for the application designers (or maybe they’re just lucky). Now attention turns to a more granular examination of the

# Chapter 1: Introduction to Web Applications Security

components of the application itself—what sort of content runs on the server? Surveying a Web application attempts to discern what application technologies are deployed (ASP, ISAPI, Java, CGI, others?), the directory structure and file composition of the site, any authenticated content and the types of authentication used, external linkage (if any), and the nature of back-end datastore (if any). This is probably one of the most important steps in the methodology, as oversights here have significant effects on the overall accuracy and reliability of the entire application review. Surveying the application is covered in Chapter 4.

# Attack the Authentication Mechanism

If any authenticated content is discovered in the previous step, it should be thoroughly analyzed, as it likely protects sensitive areas of a site. Techniques for assessing the strength of authentication features include automated password guessing attacks, spoofing tokens within a cookie, and so on. Chapter 5 looks at Web authentication hijacking in greater detail.

# Attack the Authorization Schemes

Once you are authenticated, the next step is to access to files and other objects. This can be accomplished in various ways—through directory traversal techniques, the user principle (for example, altering form or cookie values), requesting objects with useless names, attempting canonicalization attacks, escalating privileges, and tunneling privileged commands to the SQL server. This portion of the methodology is discussed in Chapter 6.

We also discuss one of the most important aspects of authorization—maintaining state—in Chapter 7.

# Perform a Functional Analysis

Another critical step in the methodology is the actual analysis of each individual function of the application. The essence of functional analysis is identifying each function of the application (for example, order input, confirmation, and order tracking) and attempting to inject faults into each input respectively. This process of failed injection is central to software security testing, and is sometimes referred to as input validation attacks, which is the title of Chapter 8.

# Explore the Data Connectivity

Some of the most devastating attacks on Web applications actually relate to the back-end database. After all, that's usually all of the juicy customer data stored away, right? Because of the myriad of ways available to connect Web applications with databases, Web developers tend to focus on the most efficient way to make this connection, rather than the most secure. We'll cover some of the classic methods for extracting data—and even using SQL to take control of the operating system—in Chapter 9.
