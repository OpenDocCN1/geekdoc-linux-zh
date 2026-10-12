# CHAPTER 30
Using Perl

+   IN THIS CHAPTER
+   * Using Perl with Linux
+   * Perl Variables and Data Structures
+   * Operators
+   * Conditional Statements: `if/else` and `unless`
+   * Looping
+   * Regular Expressions
+   * Access to the Shell
+   * Modules and CPAN
+   * Code Examples
+   * Reference

**P**erl (Practical Extraction and Report Language) is a powerful scripting tool you can use to manage files, create reports, edit text, and perform many other tasks when using Linux. Perl is included with Fedora and could be considered an integral part of the distribution because Fedora depends on Perl for many types of software services, logging activities, and software tools. If you do a full install from this book’s DVD, you will find nearly 150 software tools written in Perl installed under the /usr/bin and /usr/sbin directories.

Perl is not the easiest of programming languages to learn because it is designed for flexibility. This chapter shows how to create and use Perl scripts on your system. You will see what a Perl program looks like, how the language is structured, where you can find modules of prewritten code to help you write your own Perl scripts, and several examples of Perl used to perform a few common functions on a computer system.

# Using Perl with Linux

Although originally designed as a data extraction and report generation language, Perl appeals to many Linux system administrators because it can be used to create utilities that fill a gap between the capabilities of shell scripts and compiled C programs. Another advantage of Perl over other UNIX tools is that it can process and extract data from binary files, whereas sed and awk cannot.

> NOTE
> In Perl, “there is more than one way to do it.” This is the unofficial motto of Perl, and it comes up so often that it is usually abbreviated as TIMTOWTDI.