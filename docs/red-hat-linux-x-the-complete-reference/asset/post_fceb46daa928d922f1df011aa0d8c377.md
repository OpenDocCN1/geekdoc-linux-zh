
Note Epiphany has replaced Galeon in Fedora Linux, but you can download current versions of Galeon from [galeon.sourceforge.net](galeon.sourceforge.net).

## Lynx and Links: Line-Mode Browser

Lynx is a line-mode browser you can use without the X Window System. A Web page is displayed as text only. A text page can contain links to other Internet resources but does not display any graphics, video, or sound. Except for the display limitations, Lynx is a fully functional Web browser. You can use Lynx to download files or to make telnet connections. All information on the Web is still accessible to you. Because it does not require much of the overhead that graphics-based browsers need, Lynx can operate much faster, quickly displaying Web page text. To start the Lynx browser, you enter `lynx` on the command line and press ENTER.

Another useful text-based browser shipped with most distributions is Links. Links is a powerful screen-based browser that includes features such as frame, form, and table support. It also supports SSL secure encryption.

## Creating Your Own Web Site

To create your own Web site, you need access to a Web server. Red Hat automatically installs the Apache Web server on its Linux systems. You can also rent Web page space on a remote server - a service many ISPs provide, some for free. On Red Hat systems, the directory set up by your Apache Web server for your Web site pages is /var/httpd/html. Other servers provide you with a directory for your home page. Place the Web pages you create in that directory. You place your home page here. You can make other subdirectories with their own Web pages to which these can link. Web pages are not difficult to create. Links from one page to another move users through your Web site. You can even create links to Web pages or resources on other sites. Many excellent texts are available on Web page creation and management.

Web pages are created using either HTML, the Hypertext Markup Language, or the newer extended version, XML, the Extended Markup Language. They are a subset of Standard Generalized Markup Language (SGML). Creating an HTML or XML document is a matter of inserting HTML or XML tags in a text file. In this respect, creating a Web page is as simple as using a tag-based word processor. You use the HTML tags to format text for display as a Web page. XML tags can include more detailed information about a particular connection such as object data or transaction characteristics. The Web page itself is a text file you can create using any text editor, such as Vi. If you are familiar with tag-based word processing on Unix systems, you will find it conceptually similar to nroff. Some HTML tags indicate headings, lists, and paragraphs, as well as links to reference Web resources.

Instead of manually entering HTML or XML code, you can use Web page composers. A Web page composer provides a graphical interface for constructing Web pages. Special Web page creation programs can easily help you create complex Web pages without ever having to type any HTML tags explicitly. Remember, though, no matter what tool you use to create your Web page, the Web page itself will be an HTML document.

Note Many of the standard editors for the K Desktop and GNOME include Web page construction features. Many enable you to insert links or format the adjoining text. For example, the KEdit program

![](img/32a48d8db4c23e6e2eb70d1e5034c976_322_0.png)

## ABC Amber CHM Converter Trial version

Please register to remove this banner.

http://www.processestext.com/abchm.html

## Java for Linux: Blackdown

To develop Java applications, use Java tools, and run many Java products, you must install the Java 2 Software Development Kit (SDK) and the Java 2 Runtime Environment (JRE) on your system. Together, they make up the Java 2 Platform, Standard Edition (J2SE). Sun currently supports and distributes Linux versions of these products. You can download them from Sun at java.sun.com/j2se and install them on your system. You can even select an RPM package version for easy installation on Red Hat. The current version of the J2SE is known as Java version 1.4. An earlier version, 1.2, will not work on Red Hat 7.0, though 1.3 will work on 7.1 and up.

Though Sun supports Linux versions of Java, more thorough and effective Linux ports of Java can be obtained from the Blackdown project at www.blackdown.org. The Blackdown project has ported the J2SE, including versions 1.4 of the SDK and JRE. They have also ported previous versions of Java, including 1.1, 1.2, and 1.3. More information and documentation is also available at this Blackdown Web site. The SDK and JRE 1.4 are usually available in the form of compressed archives, .tar.bz2. You use the `bunzip2` command to decompress the file and the tar `xvf` command to extract it. Extraction should be done in the `/usr/local` directory. Follow the instructions in the `INSTALL` file to install the software.

Numerous additional Java-based products and tools are currently adaptable for Linux. Tools include Java 3D, Java Media Framework (JMF), and Java Advanced Imaging (JAI), all Blackdown projects (see Table 14-3). Many of the products run directly as provided by Sun. These include the HotJava Web browser and the Java Web server. You can download several directly from the Sun Java Web site at java.sun.com.

Table 14-3: Blackdown Java Packages and Java Web Applications

| Application | Description |
|---|---|
| Java 2 Software Development Kit (SDK) 1.4 | A Java development environment with a compiler, interpreters, debugger, and more. Part of the Java 2 Platform. Download the Linux port from www.blackdown.org |
| Java 2 Runtime Environment 1.4 (J2RE) | A Java Runtime Environment used to run Java applets. Part of the Java 2 Platform. Download the Linux port from www.blackdown.org |
| Java 2 Platform SE (J2SE) for Linux 1.4 | Java 2 Platform, Standard Edition, which includes Java 2 SDK and RE. Download the Linux port from www.blackdown.org |
| Java 3D for Linux | Sun's 3D Application Program Interface for 3D Java programs. Download the Linux port from www.blackdown.org |
| Java Media Framework (JMF) for Linux | Enable audio and video to be added to Java. Download the Linux port from www.blackdown.org |
| Java Advanced Imaging (JAI) for Linux | Java Advanced Imaging API. Download the Linux port from www.blackdown.org |
| Java 1.1 Development Kit (JDK) and Java 1.1 Runtime Environment (JRE) | The older Java 1.1 development environment with a compiler, interpreters, debugger, and more. Download the Linux port for your distribution's update through www.blackdown.org |
| HotJava browser | Sun's HTML 3.2- and JDK 1.1-compliant Web browser. Download the Linux version from java.sun.com |
| Java Web Server | A Web server implemented with Java. Available at Java Web site at java.sun.com. |
| GNU Java Compiler | GNU Public License Java Compiler (GJC) to compile Java programs, gcc.gnu.org/java. |

Note See java.sun.com/products for an extensive listing of Java applications.

## The Java 2 Software Development Kit: SDK

The Java Software Development Kit (SDK) provides tools for creating and debugging your own Java applets and provides support for Java applications, such as the HotJava browser. The kit includes demonstration applets with source code. You can obtain detailed documentation about the SDK from the Sun Web site at java.sun.com. Three major releases of the SDK are currently available-1.2, 1.3, 1.4.-with corresponding versions for the Java 2 Runtime Environment (J2RE) for 1.2, 1.3, and 1.4. The Java SDK adds capabilities for security, GUI support with JFC (also known as Swing), and running Java enhancements, such as Java 3D and Java Sound.

The SDK includes standard features found in the JDK features for internationalization, signed applets, JAR file format, AWT (window toolkit) enhancements, JavaBeans component model, networking enhancements, a math package for large numbers, database connectivity (JDBC), object serialization, and inner classes. Java applications include a Java compiler (javac), a Java debugger (jdb), and an applet viewer (appletviewer). In addition, the SDK offers the Java Naming and Directory Interface (JNDI), integrated Swing, Java 2D, network and security enhancements, and CORBA. With SDK, you can run the Blackdown port of Java 3D, Java Advanced Imaging, Java Media Framework, and Java Sound. Detailed descriptions of these features can be found in the SDK documentation.

You create a Java applet much as you would create a program using a standard programming language. You first use a text editor to create the source code, which is saved in a file with a .java extension. Then you can use the javac compiler to compile the source code file, generating a Java applet. Numerous integrated development environment (IDE) applications are available for composing Java applets and applications. Although most are commercial, some provide free shareware versions. An IDE provides a GUI interface for constructing Java applets. You can link to and download several IDE applications through the Blackdown Web page.
