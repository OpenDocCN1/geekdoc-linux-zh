
# HTML, the New User Interface

The "pseudo-GUI" of HTML is good enough for users. It has all the required features of a full-blown GUI, such as a desktop metaphor. With HTML, if you need a popup window, you simply insert a hyperlink that makes another browser session open. If a user wants several HTML-based applications running at one time, he or she opens additional browser windows. As you've seen, HTML also has check boxes, radio buttons, and dropdown lists.

Yes, the full GUI of an applet or client/server application is more sophisticated, but the extra programming required to handle window events adds considerable programming effort to both development and maintenance. It is far easier to use HTML as the user interface, with Java servlets to handle the input, perform the business logic, and respond to the user, than to develop true GUI applications.

# End of Chapter Review

# Key Terms

| Applets | HTTP | Stateful Protocol |
| Common Gateway Interface | HTTP Headers | Stateless Protocol |
| Dynamic Information Retrieval | HttpSession Object | Web |
| Get | Java | |
| HTML | Post | |
| HTML Tags | Secured Sockets Layer | |

# Review Questions

- 1. JAVA is generally accepted to be an acronym for what term?
- 2. Define the term "applet."
- 3. A request is sent to the server when a user keys a URL into his browser or when he clicks a hyperlink.
- 4. How does a web server know when to invoke a Java servlet instead of simply returning static HTML?
- 5. Define the term "HTML tag."

# Programming Assignment

# Exercise 1: Understand HTTP

- 1. From a terminal session, use the telnet utility to perform an HTTP GET request for the file index.html from www.ibm.com:

```
$ telnet www.ibm.com 80
$ get /index.html
```

2. Notice how the connection was closed. HTTP connections always close after the response was sent back to the requesting client.

3. Using the PageUp key, review the HTML file returned from IBM's Web site.

    - A. Notice the opening HTML tag.
    - B. What HTTP status code was returned?

4. Request the same file from IBM again, but this time, you are using HTTP version 1.0:

```
$ telnet www.ibm.com 80
$ get /index.html HTTP/1.0
```

5. Review the first dozen or so lines returned by IBM's Web server. This time, because you used to use HTTP version 1.0, IBM returned a set of HTTP document headers. From this information, answer the following questions:

    - a) What HTTP server is IBM using?
    - b) What type of data is contained in the HTTP packet?
    - c) When was index.html last updated?
    - d) How many bytes of data were returned to your telnet request?

# Exercise 2: Create an HTML Page

- 1. Create the HTML file shown in Figure 6.7, and name it Panel.html.
- 2. Access the HTML file from Netscape Navigator.
- 3. Add additional input fields to the form:

    - a) Add another text field.
    - b) Add another set of radio buttons.
    - c) Add another select list.
    - d) Add another set of check boxes.
    - e) Add another submit button that displays the word Delete.

# 7

# Server-side Java

Java is a programming language introduced by Sun Microsystems in 1996. It was originally used for creating the native mode of browser-based applications known as applets. Users, however, quickly tired of the slow download times associated with Java applets. In 1998, Sun introduced the servlet specification. Today, the predominant use for Java is in server-side applications.

Java has become the ubiquitous language of network computing for many reasons. Here are a few of the more important ones:

- Object orientation—Java is an OO (object-oriented) language that improves reliability and reusability of code. Many computer languages today are OO, C++ and SmallTalk. Even legacy languages like COBOL are evolving into OO-capable languages. One of the benefits of Java is that it is designed from the beginning as an object-oriented language, so it strongly enforces OO rules.
- Small executables—Java generates very small executables, which means it is well-suited to an environment where application code needs to be downloaded from the server to a client machine.
- Security—Java programs execute within the Java virtual machine (JVM) instead of the native mode of the client operating system. Therefore, Java cannot corrupt memory outside its process space. For example, a Java program that runs in a Web browser cannot access anything that the client machine doesn't grant it to. This kind of Java program (an applet) can't even perform I/O.
- Machine-independence—Since Java code runs through a JVM, and JVMs are available on most computers (through browsers or natively through the operating system), you write your Java code once, for all platforms.
- Simplicity—Similar to C++, Java is simpler. Many of the complexities of C++ have been removed. For example, in Java, you don't need to be concerned about memory allocation and deallocation, and you don't have to work with pointers. While this allows for portability, the downside is that Java programs are interpreted, so they run more slowly than native executable code. A technique known as Just-in-Time compilation (JIT), however, can improve a Java program's performance. When a Java program is received by a client computer, the JIT compiler converts it into a native program.

# How Java Works

When you compile a Java program, the compiler does not create an executable program for the particular architecture of the machine on you're compiling. Instead, the Java compiler creates what is known as Java byte code. These byte codes are instructions that a Java virtual machine understands and executes. JVMs become available in Netscape Navigator 2.0 and Microsoft Internet Explorer 3.0. All major computer operating systems also offer JVMs.

There are three types of Java programs:

- Applets are programs written to run in a Web browser. Applets are actually launched from an HTML document through special embedded HTML statements.
- Applications, unlike Java applets, do not run from a Web browser. Instead, they run on the computer like a native program. For example, the JVMs available for Linux allow you to run Java applications from a Linux command line.
- Servlets run, not from a browser or from a command line, but from a Web application server, your...
