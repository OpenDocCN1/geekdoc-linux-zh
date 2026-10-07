So far in this section we’ve looked at a number of popular programming languages and their support under Linux. Maybe you’re not a big fan of C, C++, awk, Perl, or Tcl. Maybe you really want to program in Ada or FORTRAN on your Linux box. Don’t give up hope. Linux has a wide variety of language compilers and support tools that have been ported to work under this operating system. This chapter takes a brief tour of the languages you can find and where to get them.

We can’t possibly hope to cover every language available for Linux: there are new ports and language developments made almost weekly. However, we’ve taken a list of the most popular languages and gone from there.

# ## Ada

The Ada language is in widespread use in military applications and has gained acceptance over the last decade. With the popularity of the language among defense-related application programmers, it was inevitable that several ports of Ada would appear for Linux. The most popular version of Ada for Linux is the GNAT (Gnu Ada Translator) package developed and primarily supported through New York University. For information about the GNAT project or for information on the latest releases of GNAT, send email to gnat-request@cs.nyu.edu. The current version of GNAT is available from several FTP sites and will need to be compiled on your Linux system using the GNU C compiler.

> **TIP**
Several FTP sites mirror the NYU GNAT archive. You can find the most recent version of GNAT at the FTP site tsx-11.mit.edu in the directory `/pub/linux/packages/ada`.

GNAT covers both the Ada83 and Ada90 standards for the Ada language and is compatible with some commercial Ada compilers.

# ## COBOL

COBOL has been around for decades and it is likely that there is more COBOL code written in the world than any other language. There are several commercial ports of COBOL compilers available for Linux, most notably the COBOL-85 port from Acucobol (see http://www.acucobol.com for more information). To date no public domain version