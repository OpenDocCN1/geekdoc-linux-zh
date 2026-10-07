Every expression that uses division, every array construction, and every would require an exception-handling mechanism.

The compiler and JVM define runtime exceptions to be the java.lang.RuntimeException class, as well as all its subclasses. Figure 5.1 shows the big picture of the exception hierarchy.
Any exception that does not descend from RuntimeException is known as a checked exception, or it is the checked exception that is handled by the try-catch mechanism. The compiler ensures that every checked exception has a handler somewhere.

Errors, which appear on the right side of the figure, behave just like other checked exceptions. However, programmers should never throw or catch errors, which are mostly troubling in JVM. The only errors that programmers are likely to see are assertion errors, which are discussed later in chapter.

# FIGURE 5.1 The Exception Inheritance Hierarchy

![](bbox=[0.258, 0.381, 0.742, 0.613])

# The finally Block

The last catch associated with a try block may be followed by a finally block. This is a block of code, enclosed in curly (()) and preceded by the keyword finally. Here's an example:

+   1. File myfile = getmyfile();
2. String s = getStringAndHopeForAllAllDigits();
3.
4. try {
5. System.out.println("About to call.");
6. int x = Integer.parseInt(s);
7. myFile.getCanonicalFile();