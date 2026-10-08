Not all Java programs are written to traverse the network. Many programmers use Java to create portable software. This is useful to prevent recompiles and, in some cases, rewrites, that may be necessary for other languages to run on different computer platforms.

# # The Java Platform

A platform is typically the hardware and software environment in which a program runs. In contrast, the Java platform is a software-only platform that runs on top of other hardware platforms.

Java consists of two components, the JVM and the Java Application Programming Interface (Java API).

The JVM, which has been previously discussed, is part of what makes a Java program portable. JVM's are not portable, they must be written for a specific computer platform. JVM's interpret the Java bytecode into machine dependent code for execution. A Java program can not be run on a computer system unless it has a JVM.

The Java API is a large collection of frequently used software components. The Java API's are grouped into libraries or packages of related components. The Java API's enable quick development by providing pre-written components for use by a developer.

Figure 14-35 shows a Java program running on a Java platform. It illustrates how the Java API's and JVM insulate the program from computer platform dependencies.