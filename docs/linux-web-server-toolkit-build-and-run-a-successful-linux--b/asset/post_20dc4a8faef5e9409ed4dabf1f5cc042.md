
# Chapter 14: Additional Information Services 387

You can learn more about WAIS and the FreeWAIS software that lets you set up indexed searchable server yourself by searching for WAIS in the Yahoo index at http://www.yahoo.com.

# Summary

In this chapter, you've learned a little about the services beyond the World Wide Web that you can include on your Web site, or at least link to your Web pages. The most popular services (FTP and e-mail) were described in more detail. In this chapter you learned:

- Many information services are used on the Internet such as FTP, e-mail, newsgroups, and gopher. These can all be accessed by most browsers. Including these services on your Linux server may add value for your users.

- FTP is the most efficient way to transfer large files over the Internet. The FTP server is set up automatically in OpenLinux and can be accessed by browsers using an FTP-style URL.

- E-mail links allow users to send messages from their browsers. Forms can also be used when a client doesn't have direct e-mail access, but this requires a script and an e-mail server on your Linux system.

- Newsgroups continue to be a popular information service that can be viewed in the latest browsers. A news server adds little value to most Web pages, but can be provided as a service to users.

- WAIS, gopher, and other information services are also used less frequently because the information available on these services is also available directly via the Web or FTP sites.

In the next part of this book, you'll learn about advanced features that you can add to your Web site to make it more secure, more useful and more fun for you and your users.

# Part IV

## Adding Advanced Features to Your Web Server

The technology available for Web sites continues to grow. With a Web site up and running smoothly, you can now add some of the more advanced features described in the chapters that follow. These features provide additional information and security for you, and additional enjoyment and productivity for visitors to your site. Some of the things described in these chapters are common today on large Web sites; others may not be widely implemented until the near future.

# Chapter 15

## Using Java and JavaScript

JAVA IS PROBABLY the most talked about development tool in years. It's the answer to so many problems in computing today, we're told. It's certainly used extensively in Web sites all over the world. This chapter gives you a brief introduction to Java and how it can be used in your Web site plans. Topics in this chapter include the following:

- The difference between Java and JavaScript
- Using JavaScript
- Using Java

# Java or JavaScript?

Both Java and JavaScript are mentioned regularly and often interchangeably. But they're not interchangeable. The first step to using either on your Web site is understanding the difference between the two.

# Understanding Java

Java is a programming language like C or Pascal or FORTRAN, names you've probably heard if you've been working with computers much. Java is a compiled language, as the others, and it's object-oriented, like C++, Smalltalk, and some less well-known languages. Java development uses a complete set of development tools, as you might have for C or Visual Basic.

Java differs from other languages when it's time to execute the program that you've written. Other languages such as Visual Basic or C create a binary executable that is designed for a particular operating system environment and microprocessor. For example, you can create – that is, and compile – a C program for your Linux system. Java programs are designed to work on many different operating systems. They are, to use a common phrase, platform-independent. They rely on a software component added to an operating system environment in order to run.

Many platforms have the ability to run Java applications because they have a Java Virtual Machine (a JVM). The JVM masks the differences between various microprocessors and operating systems to provide a common interface to the capabilities that Java programmers use. If a platform such as Sun Solaris or Windows NT has a JVM, you can run a Java program on that system just as you can run any other program. In fact, you can run the same Java program on any system that has a JVM. That means your Java applications are not tied to a single operating system or hardware platform – a huge break with the past.

This feature of Java makes it ideal for the Web. Just as a browser can download pages from a Web server and display them, the browser can download applications from a Web server and run them. This can be done regardless of the platform that the application was developed on. The only requirement is that the user has a Java-enabled browser.

# Interpreted versus Compiled Languages

Java is interpreted. But what does that mean?

When you write a program, you use keywords and an organized system based on the language you're using — Visual Basic, Pascal, or some other computer language. But the computer doesn't use that set of keywords. The computer uses numeric codes that make no sense at all to humans reading them.

The conversion from human-readable programming language to computer-usable numeric codes can take place when the program is either written or executed.

If this conversion takes place when a program is written, the program is being compiled. Conversion as the program is being executed occurs for interpreted languages — usually scripts or some types of BASIC.

The advantage of compiled languages is that they can be optimized to run efficiently when they are first created, and the source code (what the human programmer wrote) can't be seen. Interpreted languages are much slower, because each line of code must be converted when the program is run. But interpreted languages have the advantage of being cross-platform. For example, any computer with a version of the interpreter can run the program. Until Java, no widely accepted language had that advantage.

![](img/e01f1106dd2902613fa07890c8baa7e6_419.png)

# Chapter 15: Using Java and JavaScript

# Understanding JavaScript

Netscape originally had a scripting language that allowed browsers to interact directly with a user without interaction from a script on a Web server. At the same time that this scripting language was being finalized, the Java language was gaining momentum. Through an arrangement between Sun and Netscape, the scripting language came to be JavaScript and to resemble Java to some degree.

But the resemblance is not really strong, and the two differ widely. Whereas Java is a compiled language that uses a full development environment to create a binary executable program, JavaScript is an interpreted language in which generally small scripts are embedded in HTML pages using a text editor.

JavaScript programming centers around adding small pieces of functionality to Web pages — things that can be done within a browser environment. Java programs may run in this environment but can also be designed to run standalone applications; even something like a word processor can be written completely in Java.

# Understanding JavaScript’s Limitations

Because Java and JavaScript applications can be placed on a Web server and run on a Web browser, they could pose a security threat. Imagine if you were browsing the Web and downloaded a Java application that formatted your hard disk or secretly searched for certain files and e-mailed them to another company.

However, because everyone regularly browses sites where they can't be certain of the intentions or integrity of the information provider, Java and JavaScript have certain limitations that permit their use without the dangers these scenarios pose.

Basically, Java and JavaScript applications can access files and other system resources, as only when run in a nonbrowser environment. When you download and run a Java application on your system, you can feel safe about files and data. This is a restriction placed on the application by the browser. Some browsers such as Netscape Communicator have configurable settings where you can set how much access a Java or JavaScript applet should have to your systems resources or to the network. For example, common settings for networking offer one of three choices: disallow any network connections, allow connections to the server from which the applet was downloaded, or allow connections to any host on the Internet.
