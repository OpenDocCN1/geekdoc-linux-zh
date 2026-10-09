libtk.a and libtcl.a will fail to build, for instance, unless you cross-compiled and installed Tcl/Tk for your target. This doesn't mean the Python build has failed. Rather, it is an indication that one of the Python components has not built successfully. You will still be able to install and use the Python interpreter and the modules that built properly on your target.

# ## Other Programming Languages

Linux, of course, supports many more programming languages. Whether you are looking for programming in Ada, Forth, Lisp, or FORTRAN, a short search on the Net with your favorite search engine should yield rapid results. A good starting point is the “Other Languages” section in Chapter 13 of Running Linux by Matthias Dalheimer and Matt Welsh (O'Reilly).

The cross-compiling and cross-development capabilities of the various language tools will need to be evaluated on a tool-tool basis, since few compilers and interpreters lend themselves well to cross-platform development.

# ## Eclipse: An Integrated Development Environment

As we have seen in previous sections, the development tools for embedded Linux are a collection of standalone command-line programs. It has long been the preference of die-hard Unix and Linux developers to create software using a simple file editor and a command-line shell to invoke the development tool. However, most embedded software developers prefer to work in an IDE that provides a common graphical interface to all the functions of the development tools.

The Eclipse project, which IBM originally created in November 2001, and which has been an independent nonprofit corporation since 2004, provides an open development platform comprised of extensible frameworks, tools, and runtimes for building, deploying, and managing software. Its popularity, openness, and rich features make it an excellent choice as an IDE for embedded Linux development. A typical display by Eclipse appears in Figure 4-5.

Instead of a monolithic IDE, Eclipse provides a modular framework on which many IDEs can be built by combining a common base and a plethora of plug-ins for various functionalities, such as the CDT plug-in for C/C++ developers and the Remote System Explorer for target management. You can read more about Eclipse on the project website at http://www.eclipse.org.

Although several other IDEs exist for Linux, no other such tool enjoys the widespread adoption of Eclipse, which is used by both commercial vendors (who base development environments on Eclipse and provide many plug-ins and extensions) and the open source community, which has extended Eclipse to support practically every need.

We will cover the installation, adaptation, and use of Eclipse in the following sections.