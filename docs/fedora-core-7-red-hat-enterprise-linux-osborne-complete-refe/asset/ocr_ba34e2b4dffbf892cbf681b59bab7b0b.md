them from Sun at **java.sun.com/j2se** and install them on your system. Java packages and applications are listed in Table 14-4.

# ### jpackage, Sun, and Java-like (java-gcj-compat)

Fedora includes numerous free Java applications and support, like Jakarta. Check the fedoraproject.org/wiki/JavaFAQ for information on how Java is implemented on Fedora. You should use the Fedora versions of Java packages, as they have been specially modified for use on Fedora. However, the main Java Runtime Environment and SDK are not included. Instead you either use an included compatible set of GNU packages (Java-like) that allow you to run Java applets, install the JRE and SDK from JPackage, or download and install the original JRE and SDK from Sun. None of these options are exclusive.

Fedora now includes a Java-like collection of support packages that enable the use of Java Runtime operations. There is no official name for this collection, though it is referred to as *java-gcj-compat*, as well as Java-like. This collection provides a free and open source environment included with Fedora, consisting of three packages: GNU Java runtime (libgcj), the Eclipse Java compiler (ecj), and a set of wrappers and links (*java-gcj-compat*).

| Application | Description |
| :--- | :--- |
| Java 2 Software Development Kit (SDK) | A Java development environment with a compiler, interpreters, debugger, and more, **java.sun.com/j2se**. SDK is part of the Java 2 platform. Download the Linux port from JPackage or directly from Sun. |
| Java 2 Runtime Environment 1.4 (J2RE) | A Java Runtime Environment used to run Java applets. Download the Linux port from **java.com** or **jpackage.org**. |
| Java 3D for Linux | Sun’s 3-D Application Program Interface for 3-D Java programs. |
| Java-like environment | The Java-like Free and Open Environment, consisting of the GNU Java runtime (libgcj), the Eclipse Java compiler (ecj), and supporting wrappers and links (*java-gcj-compat*). Included with Fedora (**fedoraproject.org/wiki/JavaFAQ**). |
| Java Advanced Imaging (JAI) for Linux | Java Advanced Imaging API. |
| Java 1.1 Development Kit (JDK) and Java 1.1 Runtime Environment (JRE) for Linux | The older Java 1.1 development environment with a compiler, interpreters, debugger, and more. Download the Linux port for your distribution’s update through **jpackage.org**. |
| Java System Web Server | A Web server implemented with Java. Available at Java Web site at **java.sun.com** (commercial). |
| GNU Java Compiler | GNU Public Licensed Java Compiler (GJC) to compile Java programs, **gcc.gnu.org/java**. Included with Fedora (libgcj). |
| Jakarta Project | Apache Software Foundation project for open source Java applications, **jakarta.apache.org**. |

# TABLE 14-4 Java Packages and Java Web Applications