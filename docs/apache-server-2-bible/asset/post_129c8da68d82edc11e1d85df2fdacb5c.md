
## 17 Running Java Servlets and JSP Pages with Tomcat

Over the last few years, Java has become the leading Web-application platform for enterprise-grade Web development needs. Many large companies refuse to consider using any platform but Java for Web development. Fortunately, Apache deals with Java quite well. Using an Apache adapter (module) it can interact with Tomcat, the official reference implementation of both Java servlet 2.2 and JSP 1.1 specification.

A *servlet* is a Java program that runs within the Java Virtual Machine (JVM) on the Web-server system. When a request for a servlet is received, a new thread is created from an already-loaded servlet. Thus, a servlet has a much smaller startup requirement than does a CGI script. Like a CGI program, a servlet can interact with HTTP requests from Web browsers, and with relational databases such as Oracle, Postgres, and MySQL, or with other external applications, and then write results in HTTP response. A servlet has access to user-supplied data, HTTP headers such as cookies, browser information, host information, and so on, just as a CGI program does.

Tomcat, an open-source Java run-time environment (called a *container*, for Java servlets), is pretty good at handling servlet requests, but there is a compromise you can establish between Tomcat and Apache. You can use an Apache module called mod_jk (it was previously called mod_jserv) to interact with Tomcat so that Tomcat can be responsible for serving the servlet requests and Apache can handle everything else.

### In This Chapter

- Installing JDK
- Installing Tomcat
- Installing mod_jk module for Apache
- Configuring Tomcat for Apache
- Configuring servlets for Apache
- Configuring your own servlets or JSP pages
- Configuring Tomcat to use Java Security Manager
- Running Java servlets via Tomcat
- Disabling Tomcat’s HTTP service

Tomcat also implements Java Server Page (JSP) support that allows you to place Java code in HTML pages with `.jsp` extensions. Pages with such extensions are parsed by the server very similarly to how PHP or ASP pages are parsed. This makes JSP very similar to PHP or Active Server Pages (ASP)—with the added advantages of having the portability of Java and the robustness of the Java Application Programming Interface (API). Actually, JSP has all the capabilities of Java servlets, but it is easier to write Java code for small programming tasks. JSP scripts are actually converted automatically into servlets by Tomcat when they are first referenced, and compiled and instantiated in the servlet container.

This chapter discusses how to make Tomcat and `mod_jk` work with Apache so that you can use servlets and JSP.

> Note: If you are not familiar with Java servlets or JSP consider reading a book on these before proceeding with this chapter. A detailed discussion of servlet or JSP is beyond the scope of this book.

## Why Use Servlets?

The advantages of running servlets versus CGI scripts, or even `mod_perl` or FastCGI applications, are:

- Servlets are truly platform-independent and therefore highly portable. All modern server platforms support Java. Therefore, deploying servlets in a hybrid network is much easier than any other Web application platform.

- Fewer overheads than a CGI program because of a smaller startup footprint. No new processes need to be spawned to service a request. Simply a new thread is created to service the new request, which has a much smaller resource cost than starting a new process.

- Database connectivity via Java Database Connectivity (JDBC) is preferable to connectivity via the Perl DBI, which has major performance issues in high-load environments. CGI scripts connect to the database every time they start up; `mod_perl` scripts can cache database connection but have no good way of managing connections. An Apache server running 50 children can potentially open 50 database connections. Because high-performance sites have many Web servers such database connection requirement alone will be impossible to manage for most RDBMS available today. The best approach is connection pooling which can be done in a `mod_perl` environment with a great deal of custom coding but it is quite simple in a servlet environment.

- Java servlets run in the Java “sandbox” (JVM), which makes them a more secure option over other Web application platforms — no more buffer overrun to worry about.

## Installing Tomcat

To install Tomcat on your server you need to have a Java Run-time Environment (JRE), and if you plan on developing servlets then you will also need Java Development Kit (JDK). Also, to use Tomcat with Apache you need the mod_jk module. In this section I discuss how to install these components to create a Tomcat server environment.

### Installing the latest JDK for Tomcat

Before you install Tomcat, you need an appropriate Java Runtime Environment (JRE). A full software development kit (SDK) is necessary if you’ll be writing and compiling your own Java servlets. The Java Development Kit (JDK), available for free from Sun Microsystems (http://java.sun.com/), includes both JRE and development packages. You can install JDK for a Linux system by following these steps:

1. Download the latest release version of JDK (that is, SDK) from the official Java Web site. As of this writing the latest version is 1.3 and it is offered as a self-extracting shell script that creates a binary RPM package. You can download the `j2sdk-1_3_0_02-linux-rpm.bin` (or a later version if available) in a directory.

2. As root, run `sh j2sdk-version-linux-rpm.bin`. For example, for the 1.3 version you can run: `sh j2sdk-1_3_0_02-linux-rpm.bin`. When this script runs it displays a license, which you should say yes to. The script unpacks and creates an RPM package called `j2sdk-version-linux-rpm` (for JDK 1.3 it is `j2sdk-1_3_0_02-linux-rpm`).

3. Run the `rpm -ihv j2sdk-version-linux.rpm` to install the JDK. For example, to install the JDK 1.3, run the `rpm -ihv j2sdk-1_3_0_02-linux.rpm` command.

4. The JDK is installed in the `/usr/java/jdkversion` directory. For example, the 1.3 JDK is installed in the `/usr/java/jdk1.3_0_02` directory. This directory is the `JAVA_HOME` directory. You should set up an environment variable called `$JAVA_HOME` to point to this directory. If you use the bash shell, you can set this in your `~/.bashrc` file as follows: `export JAVA_HOME=/usr/java/jdkversion`. For example: `export JAVA_HOME=/usr/java/jdk1.3_0_02`. Enter `echo $JAVA_HOME` in your shell prompt to determine whether this environment variable is set. If you just added it to the `.bashrc` file, then you must run `source ~/.bashrc` to export the variable.

### Installing Tomcat and the mod_jk module

After you have installed the latest release version of JDK from the official Java Web site (as described in the last section), you're ready to install Tomcat and the mod_jk module as follows:

Download the latest Tomcat binary packages from the official Tomcat Web site at http://jakarta.apache.org. As of this writing the latest release version of Tomcat is 3.2, which will change to 4.0 by the time this book is in the stores. So make sure you change the version numbers mentioned in the instructions given below.

For Linux, the latest binary RPM packages can be downloaded from `http://jakarta.apache.org/builds/jakarta-tomcat/release/v3.2.1/rpms` directory. The packages you should download for Linux are:

- `tomcat-version.noarch.rpm` (current version: `tomcat-3.2.1-1.noarch.rpm`). This is the binary distribution of Tomcat.
- `tomcat-mod-version.i386.rpm` (current version: `tomcat-mod-3.2.1-1.i386.rpm`). This contains the binary distribution of `mod_jk` and the older `mod_jserv` modules for Apache. This will install the `mod_jk.so` module in `/usr/lib/apache` directory. Because this is an Apache Dynamic Shared Object (DSO) module, you must have Apache compiled with shared object support. You can quickly check whether the Apache binary you're running has `mod.so` support. Run the `/usr/local/apache/bin/httpd -l` command to list all the modules currently compiled into Apache binary. If `mod_so.c` is not listed, you need to recompile Apache by using `--enable-module=so` option in the configure script found in Apache source distribution, and then run the `make && make install` command to reinstall Apache with DSO support.
- `tomcat-manual-version.noarch.rpm` (current version: `tomcat-manual-3.2.1-1.noarch.rpm`). This is the Tomcat document package.

> Note: If you use a different shell, such as `tcsh` or `csh`, use the `setenv JAVA_HOME /usr/java/jdkversion` command instead of the preceding `export` command.

5. Add the `$JAVA_HOME` directory in your `$PATH` environment variable using the following line in your `~/.bashrc` file.

```bash
export PATH=$PATH:$JAVA_HOME/bin
```

This line must follow the `$JAVA_HOME` line discussed in the last step.

6. Test the JDK installation by running the `java -version` command. You should see output similar to the following:

```bash
java version "1.3.0_02"
Java(TM) 2 Runtime Environment, Standard Edition (build 1.3.0_02)
Java HotSpot(TM) Client VM (build 1.3.0_02, mixed mode)
```
