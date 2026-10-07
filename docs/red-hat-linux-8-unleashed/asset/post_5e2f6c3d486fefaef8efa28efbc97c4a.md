
The first thing that acts on the list is the map operator. It transforms the list into a hash in which the keys are the list elements and the values are the lengths of each element. This is where you put in your code that does the transformation by which you want to sort.
The next operator is the sort function, which sorts the list by the values.

Finally, the hash is transformed back into an array by extracting its keys. The array is now in the desired order.

## Command Line Processing

Perl is great at parsing the output of various programs. This is a task for which many people use tools such as awk and sed. Perl gives you a larger vocabulary for performing tasks. The following example is very simple, but illustrates how you might use Perl chop some output and do something with it. In the example, Perl is used to list only files that are larger than 10KB:

```bash
$ ls -la | perl -nae 'print \$F[8] is \$F[4]\n' if \$F[4] > 10000;
```

The -n switch indicates that I want the Perl code run for each line of the output. The -a switch automatically splits the output into the @F array. The -e switch indicates that the Perl code is going to follow the command line. (Refer to the “Switches” section earlier in this chapter for more information.)

### Red Hat and Linux Commands
You'll use these commands and tools when using Perl with Red Hat Linux:
- ap—Filter used to translate awk scripts into Perl
- find2perl—A utility to create Perl code from command lines using the find command
- pcregrep—A utility to search data using Perl-compatible regular expressions
- perlcc—A compiler for Perl programs
- perldoc—A utility used to read Perl documentation
- s2p—A filter used to translate scripts into Perl
- vi—The vi (actually vim) text editor

## Reference

The first place to look is the Perl documentation and Linux man pages.
Perl, all of its documentation, and millions of Perl programs are all available free on the Internet. A number of Usenet newsgroups are also devoted to Perl, as well as shelves of books and a quarterly journal.

# CHAPTER 23 Using Perl

## Books

Although your local bookstore might have dozens of titles on Perl, the following are some of the more highly recommended of these. You might also look at the Camel Critiques (Tom Christiansen; http://language.perl.com/critiques/index.html) for reviews of other available Perl books.

- Sams Teach Yourself Perl in 21 Days, by Laura Lemay, Sams Publishing
- Sams Teach Yourself Perl in 24 Hours, Second Edition, by Clinton Perez, Sams Publishing
- Learning Perl, Third Edition, by Randal L. Schwartz, Tom Phoenix, O'Reilly & Associates
- Programming Perl, Third Edition, by Larry Wall, Tom Christiansen, and Jon Orwant, O'Reilly & Associates
- Effective Perl Programming: Writing Better Programs with Perl, by Joseph Hall, Addison-Wesley Publishing Company
- Mastering Regular Expressions, by Jeffrey Friedl, O'Reilly & Associates

## Usenet

Check out the following on Usenet:

- comp.lang.perl.misc—Discusses various aspects of the Perl programming language. Make sure that your questions are Perl-specific, not generic CGI programming questions. The regulars tend to flame folks who don't know the difference.
- comp.infosystems.authoring.cgi—Discusses authoring of CGI programs, so much of the discussion is Perl-specific. Make sure that your questions are related to CGI programming, not just Perl. The regulars are very particular about staying on topic.

## WWW

Check these sites on the World Wide Web:

- http://www.perl.com/—Tom Christiansen maintains the Perl language home page. This is the place to find all sorts of information about Perl, from its history and culture to helpful tips. This is also the place to download the Perl interpreter for your system.
- http://www.perl.com/CPAN/—This is part of the site mentioned, but it merits its mention. CPAN (Comprehensive Perl Archive Network) is the place for you to find modules and programs in Perl. If you write something in Perl that you think is particularly useful, you can make it available to the Perl community here.
- http://learn.perl.org/—One best places to start learning Perl online. If you master Perl, go to http://jobs.com/
- http://www.perlmonth.com/—A monthly e-zine dedicated to Perl. This is a fairly new venture, but already has an impressive lineup of contributors.
- http://www.hwg.org/—The HTML Writers Guild is a not-for-profit organization dedicated to assisting Web developers. One of its services is a plethora of mailing lists. the hwg-servers mailing list and the hwg-languages mailing list are great places for asking Perl-related questions.
- http://www.pm.org/—The Perl Mongers are local Perl users groups. There might be one in your area. The Perl advocacy site is http:////www.perl.org.
- http://www-106.ibm.com/developerworks/linux/library/l-p101/—A short tutorial about one-line Perl scripts and code.

## Other

One valuable resource not falling into any of the preceding categories is as follows:

> The Perl Journal (http://www.tpj.com)—The Perl Journal is a quarterly publication devoted to the Perl programming language. TPJ is always full of excellent, amusing, and informative articles, and is an invaluable resource to both new and experienced Perl programmers.

# CHAPTER 24

## Kernel and Module Management

## IN THIS CHAPTER

- The Linux Kernel
- When to Recompile
- The Linux Source Tree
- Types of Kernels
- Kernel Versions
- Getting the Kernel
- Patching the Kernel
- Compiling the Kernel
- Different Configuration Interfaces
- Making Dependencies
- Final Steps
- Building and Installing Modules
- Configuring Grub
- When Something Goes Wrong
- Kernel Tuning with sysctl
- Reference

A kernel is a complex piece of software that manages the processes and interactions that take place within an operating system. As a user, you rarely, if ever, interact directly with it. Instead, you work with the applications that kernel manages.

The Linux kernel is Linux. It is the result of years of cooperative (and sometimes contentious) work by numerous people around the world. Each Linux distribution, including Red Hat Linux, comes with its precompiled kernel as well as the kernel source code, providing you with absolute authority over the Linux Operating system. In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

[ 821]

The Linux kernel is Linux. It is the result of years of cooperative (and sometimes contentious) work by numerous people around the world. Each Linux distribution, including Red Hat Linux, comes with its precompiled kernel as well as the kernel source code, providing you with absolute authority over the Linux Operating system. In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

The Linux kernel is Linux. It is the result of years of cooperative (and sometimes contentious) work by numerous people around the world. Each Linux distribution, including Red Hat Linux, comes with its precompiled kernel as well as the kernel source code, providing you with the the the.. In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter is we. is is the of of learn what of does forand and for work.

In the distribution, distribution'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter is we..

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter is we..

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

In this chapter, we'll examine the kernel and learn what it does for us and for us.

# The Linux Kernel

The Linux kernel is Linux. It is the result of years of cooperative (and sometimes contentious) work by numerous people around the world. Each Linux distribution, including Red Hat Linux, comes with its precompiled kernel as well as the kernel source code, providing you with absolute authority over the Linux Operating system. In this chapter, we'll examine the kernel and learn what it does for us and for us.

# The Linux Source Tree

The source code for the kernel is kept in a group of directories called the kernel source tree. The structure of the kernel source tree is important because the process of compiling (building) the kernel source tree is automated; it is controlled by scripts. These scripts, known as makefiles, expect to find the pieces of the kernel code in specific places or they will not work. You learn how to use to compile a kernel later in this chapter.

It is not necessary for the Linux kernel source to be installed on your system or for you to accomplish typical tasks like electronic mail or word processing. It is necessary that the kernel sources be installed, however if you want to compile a new kernel. In the next section, we'll show you how to install the kernel source files and how to set up the special symbolic link required. That link is `/usr/src/linux-2.4`, and it's how we will refer to the directory of the kernel source tree as we examine the contents of the kernel source tree.

The `/usr/src/linux-2.4` contains the .config, the Makefile, and the Rules.make files. The .config file is the configuration of your Linux kernel as it was compiled. The other two files mentioned are part of the make program. The Rules.make
