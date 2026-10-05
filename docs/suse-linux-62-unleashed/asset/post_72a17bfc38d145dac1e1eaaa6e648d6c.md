
```python
#!/usr/bin/python
import os

def printenv(s):
    try:
        x = os.environ[s]
    except KeyError:
        print "No such environment var:", s
    else:
        print "Env var", s, "has value:", x

printenv("SHELL")
printenv("OSTYPE")
printenv("JUNK")
```

> The preceding code must be indented as shown. Python decides where the blocks of code to be executed start and end by the statement's indents (when executing a script) or blank lines (when running interactively). The def;, try;, except;, and else: statements each have subservient blocks of code.

Try this code on your system. You'll almost certainly have environment variables SHELL and OSTYPE and probably will not have JUNK.

# Java Programming

This section is introduced as a short overview of the Java programming language and platform. Java is a programming language originally developed by Sun Microsystems, Inc. Java started out being called Green and then later changed to Oak, inspired by the tree outside the office window of one of the designers. Java was originally meant to be develop software for consumer electronics. The idea was that VCRs and microwaves used many different microprocessors and embedded operating systems. The designers felt there had to be an easier way to develop software for these appliances and to ultimately make them talk to one another.

# SuSE Linux Programming Tools
CHAPTER 25

This solution eventually became known as Java. Java found a new use once the Internet craze hit. Somebody realized that Internet applications had the same problem as consumer appliances. Many different platforms were all interconnected via the Internet and Wide Web and Java connected them even further by allowing them to share and execute the same programming instructions.

HTML was platform-independent. It did not matter what machine, operating system, or Web browser you had. The Web grew its hyperlink text and there was a need for more sophisticated users of the World Wide Web: to deliver dynamic real-time data and applications. The Java designers decided to embed Java in a Web browser, and the Java applet was born. Now you could load a Java page embedded with a small, platform-independent program written in the Java language.

# Uses of Java

Java has many uses. It provides many features that other languages provide and is also a platform that contains the Java Base API. The Base API was designed to be a common set of APIs for Java. These APIs consist of reusable objects that most developers need to develop their applications.

This set of common libraries extends Java's uses even further. The Java Base API includes libraries for networking, distributing objects, and database connectivity. The Java Base API also includes a platform-independent windowing toolkit called the Java Abstract Windowing Toolkit for writing graphical user interfaces.

Java's biggest momentum right now seems to stem from the enterprise. Big corporations seem to be amazed by its platform independence and easy integration with other environments. Java is quickly growing as a solution to complex business problems. Some of the new APIs and specifications that are being developed for Java make it ideal. Java makes it easy to integrate with existing databases via the JDBC (Java Database Connectivity) API, and now specifications as Enterprise JavaBeans are built around standards such as CORBA (Common Object Broker Architecture) that can integrate with existing systems. Enterprise Java Beans is an extension of Java's component architecture, Java Beans. Enterprise Java Beans enhances Java Beans by making it distributed and persistent.

# Note

JavaScript is a scripting language developed by Netscape. JavaScript is normally used as script embedded in HTML that Web browsers interpret. Java and JavaScript are completely different.

![](img/cbac72550c7126a22162e94d91a0c360_842_0.png)

# Graphics, Multimedia, and Productivity Tools
PART IV

Java is also finding many uses for Web applications. Java was originally touted out as little applets that could be run in your Web browser, but more and more people are finding that Java can be used on the server side via servlets. These servlets are replacing Web server CGI scripts that were traditionally written in languages such as Perl and C/C++.

# The Java Virtual Machine

To run code for the Java platform requires a piece of software that is commonly referred to as the Java Virtual Machine. This piece of software adds an abstraction layer to the underlying operating system and hardware of a particular platform.

Many languages are compiled into machine code that can be executed directly on the machine's hardware. This kind of compilation is specific to the platform and can consequently only be run on hardware. For example, a C program compiled for Windows can run only under the Windows platform.

# Byte Code

What sets Java apart from many other technologies? Java is not compiled into machine code for a specific platform. Java is compiled into platform-independent byte codes, which are instructions for a platform that does not physically exist as a computer. These byte codes are designed to run for a virtual machine.

# How the JVM Protects the Underlying Operating Environment

Each platform has a different implementation of the Java Virtual Machine, and all implementations should be able to run the architectural-neutral byte codes per the Java specifications. This makes the portability of Java possible by hiding the underlying system specifics in the Virtual Machine and making it possible to run Java applications on other platforms without even recompiling. Developers can write and compile their Java applications under one platform, then deploy and run them on a totally different one.

> Platforms That Support Java (Incomplete List)

- Linux
- UNIX (Solaris, AIX, HP-UX, UNIXWare, IRIX, and so on)
- Windows 95/98/NT
- IBM OS/390, OS/400, OS/2
- MacOS

SuSE Linux Programming Tools
CHAPTER 25

# Applications Versus Applets

Applications applets are the two basic types of programs you can run in Java. Java applications are very similar to other applications that are written in C++, Visual Basic, or any other language. Applications are typically installed on your workstation and executed via a command-line and as standalone programs.

On the other hand, Java applets are small programs that are designed to run in a Web browser and dynamically loaded over the network to be executed on your workstation. Java applets are typically seen embedded in Web pages that perform some small task.

When a user writes a Java applet, he or she adds functionality to the applet.Applet object is a generic applet that the Web browser recognizes. Extending the generic Java applet gives your applet the advantage of running in a feature-rich environment.

A very important feature of applet is what it makes unique from applications is its security. Java applets run within a restricted environment. This environment prevents the applet from performing any malicious acts on your workstation, such as removing all the files from your hard disk.

# Cross-Platform Development Versus Proprietary Development

Cross-development is more important than ever since the evolution of the Internet. We are in the midst of an information boom. Overnight, we have the ability to do our banking from our home, which just a few years ago would have seemed feasible only if you were a banker. We can trade stocks, find out what the current weather is, and track the packages we have shipped.

Say you log on to the Internet to your bank to transfer money into your checking account. The computers, software, and architecture that your bank use for its information systems are almost always different from the one you use at. Could you imagine having to purchase a mainframe to transfer money from your savings account to your checking? Could you imagine the bank having to write a different application for every type of platform available so you could this?

As depicted in the bank example, proprietary development can be very costly by duplicating effort and adding complexity to integration. The Internet is dependent on information and the technology it is built on changes very rapidly. Huge corporations have a wide range of different hardware and software they need to integrate.

![](img/cbac72550c7126a22162e94d91a0c360_844_0.png)
