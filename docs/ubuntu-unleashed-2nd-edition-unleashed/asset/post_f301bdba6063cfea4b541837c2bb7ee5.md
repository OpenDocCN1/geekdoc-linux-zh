
A much smarter option is to use phpLDAPadmin, which is an LDAP administration tool that allows you to add and modify entries entirely through your web browser. You can learn more and download the product to try at http://www.phpldapadmin.com.

## Reference

- <http://www.openldap.org> — The home page of the OpenLDAP project where you can download the latest version of the software and meet other users.
- <http://www.kingsmountain.com/ldapRoadmap.shtml> — A great set of links and resources across the Internet that explain various aspects of LDAP and its parent protocol, X.500.
- <http://ldap.perl.org/> — The home of the Perl library for interacting with LDAP provides comprehensive documentation to get you started.
- <http://www.ldapguru.com/> — A gigantic portal for LDAP administrators around the world. From forums dedicated to LDAP to jobs specifically for LDAP admins, this site could very well be all you need.

The definitive book on LDAP is *LDAP System Administration* (O’Reilly), ISBN: 1-56592-491-6. It is an absolute must for the bookshelf of any Linux LDAP administrator. For more general reading, try *LDAP Directories Explained* (Addison-Wesley), ISBN: 0-201-78792-X. It has a much stronger focus on the Microsoft Active Directory LDAP implementation, however.

## Part IV: Programming Linux

### In This Part

- CHAPTER 27 Using Perl 619
- CHAPTER 28 Working with Python 641
- CHAPTER 29 Writing PHP Scripts 659
- CHAPTER 30 C/C++ Programming Tools for Ubuntu 693

## Chapter 27: Using Perl

Perl (the Practical Extraction and Report Language, or the Pathologically Eclectic Rubbish Lister, depending on who you speak to), a powerful scripting tool, enables you to manage files, create reports, edit text, and perform many other tasks when using Linux. Perl is included with Ubuntu and could be considered an integral part of the distribution because Ubuntu depends on Perl for many types of software services, logging activities, and software tools. If you do a full install from this book’s disc, you will find nearly 150 software tools written in Perl installed under the /usr/bin and /usr/sbin directories.

Perl is not the easiest of programming languages to learn because it is designed for flexibility. This chapter shows how to create and use Perl scripts on your system. You will see what a Perl program looks like, how the language is structured, and where you can find modules of prewritten code to help you write your own Perl scripts. This chapter also includes several examples of Perl used to perform a few common functions on a computer system.

### In This Chapter

- Using Perl with Linux
- Perl Variables and Data Structures
- Operators
- Conditional Statements: if/else and unless
- Looping
- Regular Expressions
- Access to the Shell
- Modules and CPAN
- Code Examples
- Reference

### Using Perl with Linux

Although originally designed as a data-extraction and report-generation language, Perl appeals to many Linux system administrators because it can be used to create utilities that fill a gap between the capabilities of shell scripts and compiled C programs. Another advantage of Perl over other UNIX tools is that it can process and extract data from binary files, whereas sed and awk cannot.

> **NOTE:** In Perl, "there is more than one way to do it." This is the unofficial motto of Perl, and it comes up so often that it is usually abbreviated as TIMTOWTDI.

You can use Perl at your shell's command line to execute one-line Perl programs, but most often the programs (usually ending in .pl) are run as a command. These programs generally work on any computer platform because Perl has been ported to just about every operating system. Perl is available by default when you install Ubuntu, and you will find its package files on the DVD included with this book.

Perl programs are used to support a number of Ubuntu services, such as system logging. For example, the logwatch.pl program is run every morning at 4:20 a.m. by the crond (scheduling) daemon on your system. Other Ubuntu services supported by Perl include the following:

- Amanda for local and network backups
- Fax spooling with the faxrunq program
- Printing supported by Perl document filtering programs
- Hardware sensor monitoring setup using the sensors-detect Perl program

### Perl Versions

As of this writing, the current production version of Perl is 5.8.8 (which is Perl version 5 point 8, patch level 8).

You can download the code from http://www.perl.com and build it yourself from source. You will occasionally find updated versions in APT format for Ubuntu, which can be installed by updating your system. See Chapter 7, “Managing Software,” to see how to quickly get a list of available updates for Ubuntu.

You can determine what version of Perl you installed by typing perl -v at a shell prompt. If you are installing the latest Ubuntu distribution, you should have the latest version of Perl.

### A Simple Perl Program

This section introduces a very simple sample Perl program to get you started using Perl. Although trivial for experienced Perl hackers, a short example is necessary for new users who want to learn more about Perl.

To introduce you to the absolute basics of Perl programming, Listing 27.1 illustrates a simple Perl program that prints a short message.

**Listing 27.1: A Simple Perl Program**

```
#!/usr/bin/perl
print "Look at all the camels!\n";
```

Type that in and save it to a file called trivial.pl. Then make the file executable using the chmod command (see the following sidebar) and run it at the command prompt.
