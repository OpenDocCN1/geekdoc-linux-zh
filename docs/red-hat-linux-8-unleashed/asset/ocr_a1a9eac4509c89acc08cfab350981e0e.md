# CHAPTER 23

# Using Perl

# IN THIS CHAPTER

+   * Using Perl with Red Hat Linux
* Perl Variables and Data Structures
* Operators
* Conditional Statements: if/else and unless
* Looping
* Regular Expressions
* Access to the Shell
* Switches
* Modules and CPAN
* Code Examples
* Reference

Perl (Practical Extraction and Language) is a powerful scripting tool you can use to manage files, create reports, edit text, and perform many other tasks when using Red Hat Linux. Perl is included with Red Hat Linux and could be considered an integral part of the distribution, software services, as Red Hat depends on Perl for many types of services, logging activities, and software tools. If you do a full install from your book's CD-ROMs, you'll find nearly 200 software tools written in Perl installed under the /bin, /usr/bin, /usr/sbin, and /sbin directories.

Following the birth of the World Wide Web in the early 1990s, Perl took off as the language of choice for Common Gateway Interface (CGI) programming, which is used to extend features of Web sites and make the Web more than just a resource for document publishing. With the recent interest in the Open Source movement, Perl has gotten as much press as Linux, although many experienced Linux users have been using Perl for quite some time.

Perl is perhaps not the easiest of programming languages to learn because it's designed to be so flexible. This chapter shows how to create and use a Perl script on your Red Hat system. You will see what a Perl program looks like, how the language is structured, where you can find modules of prewritten code to help you write your own Perl scripts, and several examples of Perl used to perform a few common functions on a computer system.

# Using Perl with Red Hat Linux

If you're familiar with some other programming languages, chances are you can write functional Perl code. Perl contains the best features of C, BASIC, and a variety of other programming languages, with a hearty dollop of awk, sed, and shell