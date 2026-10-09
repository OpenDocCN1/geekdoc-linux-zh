# **Jtux: A Java/Jython Interface to Standard UNIX Functions**

Thirty years ago, when UNIX was new, almost all UNIX application programming was in C, and C is still the "UNIX language," in that the principal UNIX standards use C, UNIX kernels are written in C, and most UNIX programming books, such as this one, show all their examples in C. Today, however, much, if not most, UNIX programming is in anything but C: C++, Java, Perl, Python,<sup>1</sup> PHP, and so on.

C++ is a special case because you can use the C interface directly, or a very thin C++ class library such as Ux, described in Appendix B. The other languages typically provide interfaces to some classic UNIX system calls that were in POSIX.1990 but not to newer calls like getaddrinfo or msend. So, serious students who want to learn UNIX are forced to learn C or C++, even if they use Java for all their other course work, and developers don't have ready access to system calls they may need.

To solve the problem for Java, I created Java-to-Unix (Jtux). The goals of Jtux are to provide:

+   *   An educational tool for learning UNIX programming with Java or Jython.
+   *   Access to UNIX features that are currently unsupported by Java packages.
+   *   Consistent error handling. An error from a system call, no matter how it's indicated (-1 return, NULL return, error-code return, etc.) always results in throwing a `ErrorException`.

Jtux does not:

> 1. Jython is an implementation of Python, written in Java, that runs in the Java environment, so any Java class can be accessed directly. For example, in Jython you write your user interface using AWT or Swing, rather than with Tkinter. That's why Jtux works with Jython just as well as with Java. For more on Jython, go to www.jython.org.