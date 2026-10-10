
True to its origin as a system administration tool, Perl has been popular with UNIX system administrators for many years. More recently, when the World Wide Web (or Web for short) became popular and the need for Common Gateway Interface (CGI) programs arose, Perl became the natural choice for those already familiar with the language. The recent surge in Perl's popularity is primarily due to the use of Perl in writing CGI programs for the Web. Of course, as people pay more attention to Perl, they discover that Perl is useful for much more than CGI programming. That, in turn, has made Perl even more popular among users.

Perl is available on a wide variety of computer systems because, like the Linux operating system, Perl can be distributed freely.

If you are familiar with shell programming or the C programming language, you can pick up Perl quickly. If you have never programmed, becoming proficient in Perl may take a while. I encourage you to start with a small subset of Perl's features and to ignore anything you don't immediately understand. Then, slowly add Perl features to your repertoire.

## Determining Whether You Have Perl

Before you proceed with the Perl tutorial, check whether you have the `perl` program installed on your Linux system. Type the following command:

```
which perl
```

The `which` command tells you whether it finds a specified program in the directories listed in the `PATH` environment variable. If `perl` is installed, you see the following output:

```
/usr/bin/perl
```

You should find Perl already installed in all Linux distributions.

Another way to check for Perl is to type the following command to see its version number:

```
perl -v
```

Here is typical output from that command:

```
This is perl, v5.8.7 built for i586-linux-thread-multi
Copyright 1987-2005, Larry Wall
```

Complete documentation for Perl, including FAQ lists, should be found on this system using 'man perl' or 'perldoc perl'. If you have access to the Internet, point your browser at <http://www.perl.org/>, the Perl Home Page.

This output tells you that you have Perl Version 5.8, patch level 7, and that Larry Wall, the originator of Perl, holds the copyright. (Remember, however, that Perl is distributed freely under the GNU General Public License.)

![](img/11709a8f88c8cd03868a929dc94c0e2b_770_0.png)

You can get the latest version of Perl by pointing your World Wide Web browser to the Comprehensive Perl Archive Network (CPAN). The following address connects you to the CPAN site nearest to you:

```
www.perl.com/CPAN
```

## Writing Your First Perl Script

Perl has many features of C, and as you may know, most books on C start with an example program that displays Hello, World! on your terminal. Because Perl is an interpreted language, as opposed to C and C++, which require compiling before the program can be run, you can accomplish this task directly from the command line. If you enter:

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

To convert this line to a Perl script, simply place the line in a file and start the file with a directive to run the perl program (as you do in shell scripts, when you place a line such as #!/bin/sh to run the shell to process the script).

To try this Perl script, follow these steps:

- 1. **Use a text editor to type and save the following lines as a file named hello.pl:**

```perl
#!/usr/bin/perl
# This is a comment.
print "Hello, World!\n";
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_770_1.png)

- 2. Make the hello.pl file executable by using the following command:

```
chmod +x hello.pl
```

- 3. Run the Perl script by typing the following at the shell prompt:

```
./hello.pl
```

It displays the following output:

```
Hello, World!
```

That's it! You have written and tried your first Perl script.

![](img/11709a8f88c8cd03868a929dc94c0e2b_771_0.png)

Notice that the first line of a Perl script starts with #!, followed by the full pathname of the perl program. If the first line of a script starts with #!, the shell simply strips off the #!, appends the script file's name to the end, and runs the script. Thus, if the script file is named hello.pl and the first line is #!/usr/bin/perl, the shell executes the following command:

```
/usr/bin/perl hello.pl
```

## Getting an Overview of Perl

Most programming languages, including Perl, have some common features:

- Variables store different types of data. You can think of each variable as a placeholder for data — kind of like a mailbox, with a name and room to store data. The content of the variable is its value.
- Expressions combine variables by using operators. One expression may add several variables; another might extract a part of a string.
- Statements perform some action, such as assigning a value to a variable or printing a string.
- Flow-control statements enable statements to execute in various orders, depending on the value of some expression. Typically, flow-control statements include for, do-while, while, and if-then-else statements.
- Functions (also called subroutines or routines) enable you to group several statements and give them a name. Using this feature, you can execute the same set of statements by invoking the function that represents those statements. Typically, a programming language provides some predefined functions.
- Packages and modules enable you to organize a set of related Perl subroutines that are designed to be reusable. (Modules were introduced in Perl 5.)

In the next few sections, I provide an overview of these major features of Perl and illustrate the features through simple examples.

### Basic Perl syntax

Perl is free form, like C. There are no constraints on the exact placement of any keyword. Often, Perl programs are stored in files with names that end in .pl, but there is no restriction on the filenames you use.

As in C, each Perl statement ends with a semicolon (;). A hash mark or pound sign (#) marks the start of a comment: the perl program disregards the rest of the line beginning with the hash mark.

Groups of Perl statements are enclosed in braces ( { . . . } ). This feature also is similar in C.

### Variables

You don't have to declare Perl variables before using them, as you do in the C programming language. You can recognize a variable in a Perl script easily because each variable name begins with a special character: an at symbol (@), a dollar sign ($), or a percent sign (%). These special characters denote the variable's type. The three variable types are as follows:

- **Scalar variables** represent the basic data types: integer, floating-point number, and string. A dollar sign ($) precedes a scalar variable. Following are some examples:
  ```
  $maxlines = 256;
  $title = "Linux All-in-One Desk Reference For Dummies";
  ```

- **Array variables** are collections of scalar variables. An array variable has an at symbol (@) as a prefix. Thus, the following are arrays:
  ```
  @pages = (62, 26, 22, 24);
  @commands = ("start", "stop", "draw", "exit");
  ```

- **Associative arrays** are collections of key-value pairs, in which each key is a string and the value is any scalar variable. A percent sign (%) prefix indicates an associative array. You can use associative arrays to associate a name with a value. You may store the amount of disk space each user occupies in an associative array, such as the following:
  ```
  %disk_usage = ("root", 147178, "naba", 28547,
                 "emily", 55, "ashley", 40);
  ```

Because each variable type has a special character prefix, you can use the same name for different variable types. Thus, %disk_usage, @disk_usage, and $disk_usage can appear within the same Perl program.
