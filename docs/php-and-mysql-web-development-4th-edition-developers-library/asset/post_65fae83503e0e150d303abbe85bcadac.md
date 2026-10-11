
Performance, support, features (such as SQL conformance or extensions), licensing conditions and restrictions, and price all are factors to take into account. Given these considerations, MySQL has many attractive features to offer:

- Speed. MySQL is fast. Its developers contend that MySQL is about the fastest database system you can get. You can investigate this claim by visiting http://www.mysql.com/why-why-mysql/benchmarks/, a performance-comparison page on the MySQL Web site.

- Ease of use. MySQL is a high-performance but relatively simple database system and is much less complex to set up and administer than larger systems.

- Query language support. MySQL understands SQL (Structured Query Language), the standard language of choice for all modern database systems.

- Capability. The MySQL server is multi-threaded, so many clients can connect to it at the same time. Each client can use multiple databases simultaneously. You can access MySQL interactively using several interfaces that let you enter queries and view the results: command-line clients, Web browsers, or GUI clients. In addition, programming interfaces are available for many languages, such as C, Perl, Java, PHP, Python, and Ruby. You can also access MySQL using applications that support ODBC and .NET (protocols developed by Microsoft). This gives you the choice of using prepackaged client software or writing your own for custom applications.

- Connectivity and security. MySQL is fully networked, and databases can be accessed from anywhere on the Internet, so you can share your data with anyone, anywhere. But MySQL has access control so that one person who shouldn’t see another’s data cannot. To provide additional security, MySQL supports encrypted connections using the Secure Sockets Layer (SSL) protocol.

- Portability. MySQL runs on many varieties of Unix and Linux, as well as on other systems such as Windows and NetWare. MySQL runs on hardware from high-end servers down to small personal computers (even palm-pilot devices).

- Small size. MySQL has a modest distribution size, especially compared to the huge disk space footprint of certain other database systems.

- Availability and cost. MySQL is an Open Source project available under multiple licensing terms. First, it is available under the terms of the GNU General Public License (GPL). This means that MySQL is available without cost for most in-house uses. Second, for organizations that prefer or require formal arrangements or that do not want to be bound by the conditions of the GPL, commercial licenses are available.

- Open distribution and source code. MySQL is easy to obtain; just use your Web browser. If you don’t understand how something works, are curious about an algorithm, or want to perform a security audit, you can get the source code and examine it. If you think you’ve found a bug, please report it; the developers want to know.

What about support? Good question; a database system isn’t much use if you can’t get help for it. This book is one form of assistance, and I like to think that it’s useful in that regard. (The fact that the book has reached its fourth edition suggests that it accomplishes that goal.) There are other resources open to you as well, and you’ll find that MySQL has good support:

- The MySQL Reference Manual is included in MySQL distributions, and also is available online and in printed form. The Reference Manual regularly receives good marks in the MySQL user community. This is important, because the value of a good product is diminished if no one can figure out how to use it.

- Technical support contracts, monitoring services, and training classes are available from Sun.

- There are several active MySQL mailing lists to which anyone may subscribe. These lists have many helpful participants, including several MySQL developers. As a support resource, many people find these lists invaluable.

The MySQL community, developers and novices alike, is very responsive. Answers to questions on the mailing lists often arrive within minutes. When bugs are reported, the developers generally fix them quickly, and fixes become available daily over the Internet. Contrast this with the often-frustrating experience of navigating the Byzantine support channels of big vendors. You’ve been there? Me, too.

If you are in the database-selection process, MySQL is an ideal candidate for evaluation. You can try MySQL with no risk or financial commitment. If you get stuck, you can use the mailing lists to get help. An evaluation costs some of your time, but that’s true no matter what database system you’re considering — and it’s a safe bet that your installation and setup time for MySQL will be less than for many other systems.

## Already Running Another RDBMS?

If you’re currently running another database system but feel constrained by it, you definitely should consider MySQL. Perhaps performance of your current system is a concern, or it’s proprietary and you don’t like being locked into it. Perhaps you’d like to run on hardware that’s not supported by your current system, or your software is provided in binary-only format but you want to have the source available. Or maybe it just costs too much! All of these are reasons to look into MySQL. Use this book to familiarize yourself with MySQL’s capabilities, contact the MySQL sales crew, ask questions on the mailing lists, and you’ll find the answers you need to make a decision.

One thing to keep in mind is that although all major database engines support SQL, each supports a somewhat different dialect. Check the chapters in this book that deal with MySQL’s SQL dialect and data types. You may decide that the version of SQL supported by your current RDBMS is too different and that porting your applications would involve significant effort.

Part of your evaluation should be to try porting a few examples, of course. This will give you valuable experience in making an assessment. There is an ongoing commitment by the MySQL developers to an increasing conformance to standard SQL. That has the practical consequence of eliminating porting roadblocks as time goes on, so your porting effort may turn out to be easier than you expect.

## Tools Provided with MySQL

MySQL distributions include the following tools:

- **An SQL server.** This is the engine that powers MySQL and provides access to your databases.

- **Client and utility programs.** These include an interactive client program that enables you to enter queries directly and view the results. Also available are several administrative and utility programs that help you run your site: One allows you to monitor and control the server; others let you import data, perform backups, check tables for problems, and more.

- **A client library for writing your own programs.** You can write client programs in C because the library is in C, but the library also can be linked into other language processors such as Perl, PHP, or Ruby to provide the basis for MySQL interfaces in those languages.

In addition to the software provided with MySQL itself, MySQL is used by many talented and capable people who like writing software to enhance their productivity and who are willing to share that software. The result is that you have access to a variety of third-party tools that make MySQL easier to use or that extend its reach into areas such as Web site development.

## What You Can Expect from This Book

By reading this book, you'll learn how to use MySQL effectively so that you can get your work done more productively. You'll be able to figure out how to get your information into a database, and you'll learn how to get it back out by formulating queries that give you the answers to the questions you want to ask of that data.

You don't need to be a programmer to understand or use SQL. This book will show you how it works. But there's more to understanding how to use a database system properly than knowing SQL syntax. This book emphasizes MySQL's unique capabilities and shows how to use them.

You'll also see how MySQL integrates with other tools. The book shows how to use MySQL with Perl and PHP to generate dynamic Web pages created from the result of
