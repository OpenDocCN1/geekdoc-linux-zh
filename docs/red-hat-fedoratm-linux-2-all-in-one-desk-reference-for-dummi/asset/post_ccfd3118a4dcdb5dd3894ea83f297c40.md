
## Chapter 4: Programming in Perl

### In This Chapter
- Writing your first Perl program
- Getting an overview of Perl
- Understanding Perl packages and modules
- Using objects in Perl

When it comes to writing scripts, the Perl language is very popular among system administrators, especially on UNIX and Linux systems. System administrators use Perl to automate routine system administration tasks such as looking for old files that could be archived and deleted to free up disk space.

Perl is a scripting language, which means that you do not have to compile and link a Perl script (a text file containing Perl commands). Instead, an interpreter executes the Perl script. This capability makes writing and testing Perl scripts easy because you do not have to go through the typical edit-compile-link cycles to write Perl programs.

Besides ease of programming, another reason for Perl’s popularity is that Perl is distributed freely and is available for a wide variety of computer systems, including Fedora Core and many others such as UNIX, Windows 95/98/NT/2000/XP, and Apple Macintosh.

In this chapter, I introduce you to Perl scripting.

### Understanding Perl

Officially Perl stands for *Practical Extraction Report Language*, but Larry Wall, the creator of Perl, says people often refer to Perl as *Pathologically Electic Rubbish Lister*. As these names suggest, Perl was originally designed to extract information from text files and generate reports.

Perl began life in 1986 as a system administration tool created by Larry Wall. Over time, Perl grew by accretion of many new features and functions. The latest version — Perl 5.8 — supports object-oriented programming and allows anyone to extend Perl by adding new modules in a specified format.

True to its origin as a system-administration tool, Perl has been popular with UNIX system administrators for many years. More recently, when the World Wide Web (or Web for short) became popular and the need for Common Gateway Interface (CGI) programs arose, Perl became the natural choice for those already familiar with the language. The recent surge in Perl’s popularity is primarily due to the use of Perl in writing CGI programs for the Web. Of course, as people pay more attention to Perl, they discover that Perl is useful for much more than CGI programming. That, in turn, has made Perl even more popular among users.

Perl is available on a wide variety of computer systems because, like the Linux operating system, Perl can be distributed freely.

If you are familiar with shell programming or the C programming language, you can pick up Perl quickly. If you have never programmed, becoming proficient in Perl may take a while. I encourage you to start with a small subset of Perl’s features and to ignore anything you don’t immediately understand. Then, slowly add Perl features to your repertoire.

### Determining Whether You Have Perl

Before you proceed with the Perl tutorial, check whether you have the perl program installed on your Fedora Core system. Type the following command:

```
which perl
```

The which command tells you whether it finds a specified program in the directories listed in the PATH environment variable. If perl is installed, you see the following output:

```
/usr/bin/perl
```

If the which command complains that no such program exists in the current PATH, that doesn’t necessarily mean you don’t have perl installed; it may mean simply that you don’t have the /usr/bin directory in PATH. Ensure that /usr/bin is in PATH; check by typing the following command:

```
echo $PATH
```

See if the output lists the /usr/bin directory. If /usr/bin is not in PATH, use the following command to redefine PATH:

```
export PATH=$PATH:/usr/bin
```

Now, try the which perl command again. If you still get an error, you may not have installed Perl. You can install Perl from the companion DVD-ROM by performing the following steps:

- 1. Log in as root.
- 2. Insert the companion DVD-ROM in the DVD-ROM drive. If you are working in the GNOME or KDE graphical environment, the DVD-ROM mounts automatically. Otherwise, mount the DVD-ROM by typing the following command:
    ```
    mount /mnt/cdrom
    ```
- 3. Type the following command to change the directory to the location of the Red Hat packages:
    ```
    cd /mnt/cdrom/Fedora/RPMS
    ```
- 4. Type the following rpm (Red Hat Package Manager) command to install Perl:
    ```
    rpm -ivh perl*
    ```

After you install Perl on your system, type the following command to see its version number:
`perl -v`
Here is typical output from that command:

> This is perl, v5.8.3 built for i386-linux-thread-multi
> Copyright 1987-2003, Larry Wall
> Perl may be copied only under the terms of either the Artistic License or the GNU General Public License, which may be found in the Perl 5 source kit.
> Complete documentation for Perl, including FAQ lists, should be found on this system using 'man perl' or 'perldoc perl'. If you have access to the Internet, point your browser at http://www.perl.com/, the Perl Home Page.

This output tells you that you have Perl Version 5.8, patch Level 3, and that Larry Wall, the originator of Perl, holds the copyright. (Remember, however, that Perl is distributed freely under the GNU General Public License.)

You can get the latest version of Perl by pointing your World Wide Web browser to the Comprehensive Perl Archive Network (CPAN). The following address connects you to the CPAN site nearest to you:
www.perl.com/CPAN/

![](img/9f89727199836b0f871f1745838aa8b2_807_0.png)

### Writing Your First Perl Script

Perl has many features of C, and, as you may know, most books on C start with an example program that displays Hello, World! on your terminal. Because Perl is an interpreted language, you can accomplish this task directly from the command line. If you enter

```
perl -e 'print "Hello, World!\n";'
```

Perl responds with the following:

```
Hello, World!
```

This command uses the -e option of the perl program to pass the Perl program as a command-line argument to the Perl interpreter. In this case, the following line constitutes the Perl program:

```
print "Hello, World!\n";
```

To convert this line to a Perl script, simply place the line in a file, and start the file with a directive to run the perl program (as you do in shell scripts, when you place a line such as #!/bin/sh to run the shell to process the script).

To try this Perl script, follow these steps:

- 1. **Use a text editor to type and save the following lines in the file named hello.pl:**

    ```
    #!/usr/bin/perl
    # This is a comment.
    print "Hello, World!\n";
    ```

- 2. **Make the hello.pl file executable by using the following command:**

    ```
    chmod +x hello.pl
    ```

- 3. **Run the Perl script by typing the following at the shell prompt:**

    ```
    ./hello.pl
    ```

It displays the following output:

```
Hello, World!
```

That's it! You have written and tried your first Perl script.

Note that the first line of a Perl script starts with #!, followed by the full pathname of the perl program. If the first line of a script starts with #!, the shell simply strips off the #!, appends the script file's name to the end, and runs the script. Thus, if the script file is named hello.pl and the first line is #!/usr/bin/perl, the shell executes the following command:

```
/usr/bin/perl hello.pl
```

### Getting an Overview of Perl

Most programming languages, including Perl, have some common features:

- **Variables** store different types of data. You can think of each variable as a placeholder for data — kind of like a mailbox, with a name and room to store data. The content of the variable is its value.
- **Expressions** combine variables by using operators. One expression may add several variables; another might extract a part of a string.
- **Statements** perform some action, such as assigning a value to a variable or printing a string.
- **Flow-control statements** enable statements to execute in various orders, depending on the value of some expression. Typically, flow-control statements include `for`, `do-while`, `while`, and `if-then-else` statements.
- **Functions** (also called *subroutines* or *routines*) enable you to group several statements and give them a name. Using this feature, you can execute the same set of statements by invoking the function that represents those statements. Typically, a programming language provides some predefined functions.
- **Packages and modules** that enable you to organize a set of related Perl subroutines that are designed to be reusable. (Modules were introduced in Perl 5.)

In the next few sections, I provide an overview of these major features of Perl and illustrate the features through simple examples.

### Basic Perl syntax

Perl is free-form, like C. There are no constraints on the exact placement of any keyword. Often, Perl programs are stored in files with names that end in `.pl`, but there is no restriction on the filenames you use.

As in C, each Perl statement ends with a semicolon (`;`). A hash mark or pound sign (`#`) marks the start of a comment; the `perl` program disregards the rest of the line beginning with the hash mark.

Groups of Perl statements are enclosed in braces (`{ ... }`). This feature also is similar in C.
