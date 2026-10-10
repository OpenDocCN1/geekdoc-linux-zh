
- Programming Perl, Second Edition, by Larry Wall, Randal L. Schwartz, and Tom Christiansen. O’Reilly & Associates.
- Effective Perl Programming: Writing Better Programs with Perl, by Joseph Hall. Addison-Wesley Publishing Company.
- Mastering Regular Expressions, by Jeffrey Friedl. O’Reilly & Associates.
- Perl in a Nutshell: A Desktop Quick Reference, by Ellen Siever, Stephan Sphaenour, and Nathan Patwardhan. O’Reilly & Associates.

## Usenet

Check out the following on Usenet:

- comp.lang.perl.misc Discusses various aspects of the Perl programming language. Make sure your questions are Perl-specific, not generic CGI programming questions. The regulars tend to flame folks who do not know the difference.
- comp.infosystems.www.authoring.cgi Discusses authoring of CGI programs; consequently, much of the discussion is Perl-specific. Make sure your questions are related to CGI programming, not just Perl. The regulars are very particular about staying on-topic.

## WWW

Check these sites on the World Wide Web:

- http://www.perl.com/ The Perl language home page is maintained by Tom Christiansen. This is the place to find all sorts of information about Perl, from its history and culture to helpful tips. This is also the place to download the Perl interpreter for your system.
- http://www.perl.com/CPAN/ This is part of the previous site just mentioned, but it merits its own mention. CPAN is the place for you to find modules and programs in Perl. If you end up writing something in Perl that you think is particularly useful, you can make it available to the Perl community here.
- http://www.perlmonth.com/ This is a monthly e-zine dedicated to Perl. It is a fairly new venture but already has an impressive line-up of contributors.
- http://www.hwg.org/ The HTML Writers Guild is a nonprofit organization dedicated to assisting Web developers. One of their services is a plethora of mailing lists. The hwg-servers mailing list and the hwg-languages mailing list are great places for asking Perl-related questions.
- http://www.pm.org/ The Perl Mongers are local Perl users groups. There might be one in your area.

## Other

Other valuable resources not falling into any of the preceding categories follow:

- The *Perl Journal* (`http://www.tpj.com/`)
- *The Perl Journal* is a quarterly publication devoted to the Perl programming language. Orchestrated by Jon Orwant, *TPJ* is always full of excellent, amusing, and informative articles; it is an invaluable resource to new and experienced Perl programmers.

## Summary

Perl, in the words of its creator, "combines the best elements of C, `sed`, `awk`, and `sh`," and is also a great language for folks who have no experience with these languages.

Perl's powerful regex (regular expression) library and ease of use have made it one of the preferred scripting languages in use today, particularly in the realm of CGI programming. Many people even think of Perl as exclusively a CGI language, when, in fact, it is capable of so much more.

Perl is often referred to as a glue language for its ability to stick together a variety of disparate applications into something coherent. Perl can make your job as a system administrator easier by taking some of the work off your hands and by making your various applications work together.

## Introduction to Tcl/Tk

### In This Chapter

- A Quick Example 782
- “Hello, World” in Tk 783
- Tcl Syntax and Concepts 784
- Variables 787
- Expressions 789
- Lists 791
- Control Structures 794
- Procedures 797
- Tk 799
- Tcl Extensions 805
- Going Further 806

Tcl is an interpreted language developed by John Ousterhout at the University of California at Berkeley. Tcl was originally designed for “gluing” small applications (written in C or another language) together with a scripting language to form larger applications. However, Tcl was so successful that many large applications have been written entirely in Tcl. Tcl is now supported by a company called Scriptics, whose Web site is http://www.scriptics.com.

Along with Tcl, Ousterhout developed the Tk toolkit. Tk is a graphical toolkit and is one of the main reasons for the popularity of Tcl. Using Tcl and the Tk toolkit together, you can create graphical applications very rapidly. Tcl and Tk serve as excellent “wrappers” for command-line programs, turning them into attractive graphical applications.

In addition, Tcl and Tk are embeddable. You can link C libraries to your C or C++ programs, making all the capabilities of Tcl and Tk available. Thus, you can write compiled or time-critical portions of your program in C or C++ and tie them together with the Tcl scripting language. You can also develop user-interfaces using Tcl and Tk.

And if that wasn’t enough, Tcl/Tk is free software. It is not even licensed under the GPL or LGPL; you can legally embed Tcl/Tk in commercial products without paying any license fees, which is another reason for its popularity. Finally, Tcl/Tk is cross-platform—it works with very minor differences on Linux, practically all UNIX platforms, Windows, and Mac OS. This portability makes Tcl/Tk a very attractive solution for deploying cross-platform applications.

This chapter will give you a brief overview of Tcl/Tk. However, it will not teach you how to program. I assume that you have some familiarity with computer programming and understand concepts like variables, loops, if/then structures and procedures. For a detailed discussion of Tcl/Tk, read *Tcl and the Tk Toolkit* by John Ousterhout (details are in the bibliography.)

## Quick Example

Tcl/Tk programs are often called scripts. The *tclsh* program interprets Tcl scripts, while the *wish* program interprets Tcl scripts with Tk toolkit extensions.

Start *tclsh* and type `expr 2 + 3`. You should see something like the following:

```
$ tclsh
% expr 2 + 3
5
%
```

The percent sign is tclsh’s prompt. The line `expr 2 + 3` is a Tcl command. All Tcl commands consist of words separated by whitespace. In this example, the command has four words, with the first being `expr` and the last being `3`.

The first word of a command is the command name; the remaining words are the arguments. In this respect, Tcl's syntax is very similar to that of the UNIX shell.

Normally, you terminate commands with newlines. However, you can split a long command over several lines by ending each line but the last with a backslash character (`\`).

When the Tcl interpreter executes a command, the command returns a return value. After interpreting each command, *tclsh* prints the return value. In this case, the return value of *expr 2 + 3* was 5.

To exit from *tclsh*, type *exit*.

## “Hello, World” in Tk

Now let's look at some Tk extensions. The *wish* program contains the Tcl language interpreter and the Tk graphical extensions. Start *wish* and enter the following:

```
$ wish
% button .b -text "Hi, There" -command exit
.b
% pack .b
```

You should see a window similar to that shown in Figure 33.1.

![](img/df365d352a104b50fea29e59a052de4d_820_0.png)

Let's examine this script. First, notice that each command follows the usual pattern of space-separated words. The first command has six words—the text *Hi, There* is treated as a single word because of the quotes. Although the quotes allow you to put spaces in a word, they are not actually part of the word itself.

The word structure of a Tcl command is very important. Most commands demand either a certain number of words or a specific pattern of words. You must ensure that anything you want treated as a single word really is a single word. Omitting the quotes in this example would make *Hi,* and *There* be treated as separate words, and the command would return an error.

The *button* command creates a *widget*. A *widget* is simply a window, possibly with some contents and behavior. The two pieces of the command -*text “Hi, There”* and -*command exit* are configuration options. In the case of a button, the -*text* option sets the text to be displayed in the button, and the -*command* option specifies a script to be executed when the button is clicked.
