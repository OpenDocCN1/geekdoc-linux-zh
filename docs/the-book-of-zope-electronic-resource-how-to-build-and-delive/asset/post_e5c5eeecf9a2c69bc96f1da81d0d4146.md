
This combination of self-designed, freely available modules and commercial modules was marketed by DC as Principia.

The investment banker Hadar Pedhazur, user of both Python and the freely available Digital Creations software Bobo, liked Digital Creations and began speaking with its chief executive, Paul Everett, about investing Principia as open source software to guarantee the quickest market penetration. Indeed, market penetration and awareness were the biggest problems for Principia; Digital Creations had neither the marketing budget nor the high profile of other manufacturers of web application servers such as Apple (Web Objects) or Allaire (Cold Fusion).

Another reason for making Digital Creations' web application open source was that the revenues from software licensing would be negligible compared to the revenues from providing solutions to Principia. In other words, the more Principia users who changed to Zope as a result of the open source license, the more positive the effects on Digital Creations' main source of income: consulting and solutions development.

Once the decision was made to take Principia down to open source, it was time to find a new name for this open source platform. Eventually, the company chose the name Zope, which stands for "Z Object Publishing Environment."

## About the Authors

Enough about Zope and this book, it's time to introduce ourselves. We all have something in common beyond our enthusiasm for Zope: We all work for the same Berlin and Washington, D.C.-based company, Beehive, L.L.C., which has been providing Zope solutions for many years. The following "bees" lent their skills to this book: Katrin Kirchner, Martina Blockmann, Nico Grubert, Mark Pratt, Sebastian Luehsdorf, and Alexander Schad.

Special reference should be made to the work of Katrin Kirchner, Martina Blockmann, and Nico Grubert. Not only did they write the vast majority of this book, but through their electronic books (E-Books) and training courses held throughout Germany, they have also helped hundreds of developers join the Zope community. These training courses are also available through our Washington, D.C., office.

At beehive we would like to thank the staff of dpunkt.verlag and especially René Schönfeldt, who was always there for us with suggestions and constructive criticism regarding how we could improve this book.

## 1
## ZOPE FUNDAMENTALS

![](img/43a28cce5475b2f487bf455365567fb6_22_0.png)

This chapter introduces ways of using Zope for web development and as a web application and content manager server. The second half of the chapter takes you through installing Zope under the various operating systems.

### 1.1 Web Applications

The World Wide Web is no longer merely a collection of static web pages, but is increasingly becoming a transport medium for many services that blur the lines between content and software. Examples include knowledge databases and Internet search engines, as well as entirely new software categories such as content management systems (for managing and publishing content to websites or intranet portal systems (which allow Internet communities to create and exchange content)); and weblogs (news systems, usually featuring discussion forums, such as dashdot.org).

These software systems are referred to as web applications because they require only a web browser for access and no additional software. They are typically easy to use.

As the demands placed on these web applications have become increasingly complex, programmers have hit the boundaries of what can be done with traditional CGI (common gateway interface) programming, thus creating a demand for suitable alternatives. And, because web programmers have no interest in using web applications that work with CGI scripts to implement recurring basic systems as user authentication and authorization applications for ecommerce community portals, they are turning to systems like Cold Fusion, PHP 3 and 4, and Zope to provide these basic services and make software development easier.

### 1.1.1 The Advantages of Zope for Web Application Programmers

Zope has a lot to offer web application programmers:

- Zope is entirely object-oriented.
- Zope contains an integrated object-oriented database and a webserver.
- Zope is transaction-oriented and allows users to do things like undo actions and so on.
- Thanks to database adapters (DAs), Zope can be connected to relational databases such as Oracle, Sybase, PostgreSQL, and Interbase.
- Zope's extremely flexible open source license allows developers to use Zope for both their own projects and customer projects without any restriction or license fees.
- The Zope community makes available hundreds of applications just for Zope (known as Zope Products), which can be easily implemented by users with no programming knowledge using Zope's integrated web management system.
- Zope's scripting language, DTML, and ZClasses let you program Zope systems via using only your web server.
- Thanks to Python's object-oriented structure, hundreds of available modules can be integrated into Zope to allow you to perform specialized tasks, such as creating reports in PDF format.

### 1.2 Zope As a Web Application Server

A web application server functions as the bridge (middleware) among the browser, the developer's software application, and a database.

As the boundaries between websites and web applications disappear, it is more important for integrated teams of software, database, and interface developers to establish a common basis for their work. The Zope web application provides this basis, allowing you to use rich HTML, DTML, SQL, Python, and eventually even Perl Code in Zope as described.

In addition, Zope's scripting language, DTML, can be used to access a vast array of functions and perform complex actions and templating with a few lines of code. For example, to allow a group of users (subscribers, for instance) to view content different from what the “ordinary” visitor sees, you can use Zope's integrated system (Chapter 3) to see whether the user logging in belongs to a particular role or has any special permissions.

#### 1.2.1 Content-by-Role

We achieve this ability to let different user types view content-by-role. This is a fundamental function of content management systems used, for example, to provide editors with different menu options than those available to journalists.

#### 1.2.2 SQL

SQL, the Structured Query Language for databases, can also be used directly in Zope provided a suitable database adapter (DA) has been compiled beforehand. This feature allows developers to decide how much program logic to store in the database and how much to store in the Zope server.

#### 1.2.3 Python

Because Zope is mainly written using Python, it can communicate relatively easily with Python modules or programs. This feature gives programmers instant access to hundreds of modules that make it easy, for instance, to create PDF or graphics files.

### 1.3 Zope As a Content Management Server

Many organizations want the ability to structure content on their websites to make it possible for a broad spectrum of users to input and maintain content. Although web design tools such as Microsoft Front and Adobe GoLive serve this purpose, they are really suited for professional designers. People who occasionally enter a press release or a special offer to the website may find them difficult to use.

In contrast to other web applications, Zope offers a basic content management system as its web administration screen, and many of the functions of content management systems (CMS) are already integrated into Zope. An experienced programmer can use Zope to quickly build a customized CMS that, for example, displays selected Zope functions to users. Other functionality, such as staging or workflows, can be programmed later if necessary.

#### 1.3.1 Open Source Software

Zope differs significantly from commercial products. For one thing, nobody claims Zope is a product that you simply unpack, press a button, and have running with a mouse click. In fact, to date there is no thing as a ready-to-go, out-of-the-box CMS solution.

Two of Zope's major benefits in comparison with other content management systems are the facts that it is object-oriented and that it is an open source software. As object-oriented software, knowledge developed within an organization for a CMS can be quickly used to develop a portal or extranet. Because it is open source software, Zope is free—and its source code is also available to you, for free. As such, Zope has a good chance of becoming “the people's CMS” because
