
## 1.2 What Is an Interpreted Language?

Perl's heritage is UNIX. Perl scripts are functionally similar to UNIX `awk`, `sed`, shell scripts, and C programs. Shell scripts consist primarily of UNIX commands; Perl scripts do not. Whereas `sed` and `awk` are used to edit and report on files, Perl does not require a file in order to function. Whereas C has none of the pattern matching and wildcard metacharacters of the shells, `sed`, and `awk`, Perl has an extended set of characters. Perl was originally written to manipulate text in files, extract data from files, and write reports, but through continued development, it can manipulate processes, perform networking tasks, process Web pages, talk to databases, and analyze scientific data. Perl is truly the Swiss Army Knife of programming languages; there is a tool for everyone.

The examples in this book were created on systems running Solaris, Linux, Macintosh, UNIX, and Win32.

Perl is often associated with a camel symbol, a trademark of O'Reilly Media, which published the first book on Perl called *Programming Perl* by Larry Wall and Randal Schwartz (also referred to as "the Camel Book").

![](img/8556abcb353c0991f12099420ec28735_31_0.png)

To write Perl programs, you need two things: a text editor and a perl interpreter, which you can download very quickly from any number of Web sites, including `perl.org`, `cpan.org`, and `activestate.com`. Unlike with compiled languages, such as C++ and Java, you do not need to first compile your program into machine-readable code before executing it. The perl interpreter does it all; it handles the compilation, interpretation, and execution of your program. Advantages of using an interpreted language such as Perl is that it runs on almost every platform, is relatively easy to learn, and is very fast and flexible.

Languages such as Python, JavaScript, and Perl are interpreted languages that use an intermediate representation, which combines both compilation and interpretation. It compiles the user's code into an internal condensed format called bytecode, or threaded code, which is then executed by the interpreter. When you run Perl programs, you need to be aware of two phases: the compilation phase, and then the run phase where you will see the program results. If you have syntax errors, such as a misspelled keyword or a missing quote, the compiler will send an error. If you pass the compiler phase, you could have other problems when the program starts running. If you pass both of these phases, you will probably start working on formatting to make the output look nicer, improving the program to make it more efficient, and so forth.

The interpreter also provides a number of command-line switches (options) to control its behavior. There are switches to check syntax, send warnings, loop through files, execute statements, turn on the debugger, and so forth. You will learn about these options throughout the following chapters.

## 1.3 Who Uses Perl?

Because Perl has built-in functions to easily manipulate processes and files, and because Perl is portable (that is, it can run on a number of different platforms), it is especially popular with system administrators, who often oversee one or more systems of different types. The phenomenal growth of the World Wide Web greatly increased interest in Perl, which was the most popular language for writing CGI scripts to generate dynamic Web pages. Even today, with the advent of other languages focused on processing Web pages, such as Ruby, Node, and ASP.net, Perl continues its popularity with system and database administrators, scientists, geneticists, and anyone who has a need to collect data from files and manipulate it.

Anyone can use Perl, but it is easier to learn if you are already experienced in writing UNIX shell scripts or languages derived from C, such as C++ and Java. For these people, the migration to Perl will be relatively easy. For those who have little programming experience, the learning curve might be a little steeper, but after learning Perl, there may be no reason to ever use anything else.

If you are familiar with UNIX utilities such as *awk*, *grep*, *sed*, and *tr*, you know that they don't share the same syntax; the options and arguments are handled differently, and the rules change from one utility to the other. If you are a shell programmer, you usually go through the grueling task of learning a variety of utilities, shell metacharacters, regular expression metacharacters, quotes, more quotes, and so forth. Also, shell programs are limited and slow. To perform more complex mathematical tasks and to handle interprocess communication and binary data, for example, you may have to turn to a higher-level language, such as C, C++, or *Java*. If you know C, you also know that searching for patterns in files and interfacing with the operating system to process files and execute commands are not always easy tasks.

Perl integrates the best features of shell programming, C, and the UNIX utilities *awk*, *grep*, *sed*, and *tr*. Because it is fast and not limited to chunks of data of a particular size, many system administrators and database administrators have switched from the traditional shell scripting to Perl. C++ and Java programmers can enjoy the object-oriented features added in Perl 5, including the ability to create reusable, extensible modules. Now, with Perl you can generate Perl in other languages, and you can embed other languages in Perl. There is something for everyone who uses Perl, and for every task. As Larry Wall says, "There's more than one way to do it."

> 2. Larry Wall, "Diligence, Patience, and Humility." http://www.oreilly.com/catalog/opensources/book/larry.html.

### 1.3.1 Which Perl?

Perl has been through a number of revisions. The last version of Perl 4 was Perl 4, patchlevel 36 (Perl 4.036), released in 1992, making it ancient. Perl 5.000 (also ancient), introduced in fall 1994, was a complete rewrite of the Perl source code that optimized the language and introduced objects and many other features. Despite these changes, Perl 5 remains highly compatible with the previous releases. As of this writing, the current stable version of Perl is 5.20, actively maintained by a large group of voluntary contributors listed at www.ohloh.net/p/perl/contributors. Perl 6 is the next generation of another Perl redesign and does not have an official release date. It has new features, but the basic components of the Perl language you learn here will be essentially the same.

From Wikipedia:

Some observers credit the release of Perl 5.10 with the start of the Modern Perl movement. In particular, this phrase describes a style of development which embraces the use of the CPAN, takes advantage of recent developments in the language (see Table 1.1), and is rigorous about creating high-quality code.

**Table 1.1 Release Dates and Recent Developments**

| Major Version | Latest Update | Status |
| :--- | :--- | :--- |
| 5.5 | 02/23/2004 | Old version |
| 5.6 | 11/15/2003 | Old version |
| 5.8 | 12/14/2008 | Old version |
| 5.10 | 08/23/2009 | Old version |
| 5.12 | 11/10/2012 | Old version |
| 5.14 | 03/10/2013 | Old version |
| 5.16 | 03/11/2013 | Old version |
| 5.18 | 01/07/2014 | Older version, but still supported |
| 5.20 | 05/27/2014 | Current version |

> 3. Wikipedia.org, “Perl,” http://en.wikipedia.org/wiki/Perl.

### 1.3.2 What Are Perl 6, Rakudo Perl, and Parrot?

> *“Perl 5 was my rewrite of Perl. I want Perl 6 to be the community’s rewrite of Perl and of the community.”*
> —Larry Wall, State of the Onion speech, TPC4

Perl 6 is essentially Perl 5 with many new features. Although they continue to develop in parallel, Perl 6 will not supersede Perl 5. The basic language syntax, features, and purpose
