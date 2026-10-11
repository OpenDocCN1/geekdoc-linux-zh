
## 1.3 Who Uses Perl?

will be the same. If you know Perl, you will still know Perl. If you learn Perl from this book, you will be prepared to jump into Perl 6 when it is released. Perl 6 has been described by Perl.org as learning Australian English if you speak American English, rather than trying to switch from English to Chinese.

Rakudo Star, a useful and usable distribution of Perl 6 that runs on the Parrot virtual machine, was recently released in October 2013. To find out more go to http://rakudo.org.

Parrot is a virtual machine designed to efficiently compile and execute bytecode for dynamic languages. Parrot currently hosts a variety of language implementations in various stages of completion, including Tcl, JavaScript, Ruby, Lua, Scheme, PHP, Python, Perl 6, APL, and a .NET bytecode translator.

To learn more about the latest Perl core development with Perl 6, Rakudo, and Parrot, go to http://dev.perl.org (see Figure 1.1).

![](img/8556abcb353c0991f12099420ec28735_34_0.png)

Figure 1.1 The Perl 6 development Web site.

And for a biographical sketch of Larry Wall and the history of Perl, go to http://www.softwarebarn.org/People/Wall/Index.shtml#Perl_history.

## 1.4 Where to Get Perl

Perl downloading and instructions are available from a number of sources. You can check the following popular sites for a Perl distribution for your computer: *cpan.org*, *perl.org*, *activestate.com*, and *strawberryperl.com*.

> **What is Strawberry Perl?**
>
> Strawberry Perl is Perl for the Microsoft Windows platform. While most other distributions rely on the user having software development tools already set up to install certain Perl components, Strawberry Perl ships with the most commonly used tools preconfigured and packaged, including Perl binaries, the gcc compiler, all external libraries, all bundled database clients, and more. The latest version, as of this writing, is Strawberry Perl 5.20.1.1, for both 32- and 64-bit versions of Windows. (You can download it at *http://strawberryperl.com*). Larry Wall says, “When I’m on Windows, I use Strawberry Perl.”

### 1.4.1 CPAN (cpan.org)

The primary source for Perl distribution is CPAN, which is available at *www.cpan.org* (see Figure 1.2). CPAN, the “gateway to all things Perl,” stands for the Comprehensive Perl Archive Network, a Web site that houses all the free Perl material you will ever need, including documentation, FAQs, modules and scripts, binary distributions and source code, and announcements. CPAN is mirrored all over the world, and you can find the nearest mirror at

- *www.perl.com/CPAN*
- *www.cpan.org*

CPAN is the place you will go to if you want to find modules to help you with your work. The CPAN search engine will let you find modules under a large number of categories. Modules are discussed in Chapter 13, “Modularize It, Package It, and Send It to the Library!”<sup>1</sup>

Go to *www.cpan.org/ports* to find out more about what's available for your platform, of which Perl supports more than 100.

![](img/8556abcb353c0991f12099420ec28735_36_0.png)

**Figure 1.2** The CPAN Web site. Click on the Ports tab to find your platform.

### 1.4.2 Downloads and Other Resources for Perl (perl.org)

The official Perl home page, run by O'Reilly Media, Inc. is www.perl.com, but it seems that everything you will need is found at www.perl.org (see Figure 1.3).

![](img/8556abcb353c0991f12099420ec28735_37_0.png)

Figure 1.3 The Perl.org Web site.

### 1.4.3 ActivePerl (activestate.com)

If you want to install Perl quickly and easily, ActivePerl is a complete, self-installing distribution of Perl based on the standard Perl sources for Windows, Mac OS X, Linux, Solaris, AIX, and HP-UX. It is distributed online at the ActiveState site (www.activestate.com). The complete ActivePerl package contains the binary of the core Perl distribution, complete online documentation, and all the essential tools for Perl development, including PPM, a handy perl package manager. This is available at www.activestate.com/activeperl (see Figure 1.4).

![](img/8556abcb353c0991f12099420ec28735_37_1.png)

Figure 1.4 The ActiveState Web site, where you can download ActivePerl.

### 1.4.4 What Version Do I Have?

To obtain your Perl version, date the binary version was built, patches, and some copyright information, type the line shown in Example 1.1 (the dollar sign is the shell prompt).

> **EXAMPLE 1.1**
>
> $ perl -v
>
> This is perl 5, version 18, subversion 2 (v5.18.2) built for darwin-thread-multi-2level (with 2 registered patches, see perl -V for more detail)
>
> Copyright 1987-2013, Larry Wall
>
> Perl may be copied only under the terms of either the Artistic License or the GNU General Public License, which may be found in the Perl 5 source kit.
>
> Complete documentation for Perl, including FAQ lists, should be found on this system using "man perl" or "perldoc perl". If you have access to the Internet, point your browser at http://www.perl.org/, the Perl Home Page.

> **EXPLANATION**
>
> 1. This version of Perl is 5.18.2, for the Mac.
> 2. Larry Wall, the author of Perl, owns the copyright.
> 3. Perl may be copied under the terms specified by the Artistic License or GNU. Perl is distributed under GNU, the Free Software Foundation, meaning that Perl is free.

## 1.5 Perl Documentation

Today, you can find answers to any Perl questions simply by using your favorite search engine or going to the Perl.org Web site. Most Perl distributions also come with full documentation in both HTML and PDF formats.

### 1.5.1 Where to Find the Most Complete Documentation from Perl

For the most complete documentation, type the Perl function you are looking for in your search engine or just go directly to *perldoc.perl.org* (see Figure 1.5) for all the complete documentation for any version of Perl.

![](img/8556abcb353c0991f12099420ec28735_39_0.png)

**Figure 1.5** Documentation at perldoc.perl.org.

### 1.5.2 Perl man Pages

The standard Perl distribution comes with complete online documentation, called man pages, which provide help for all the standard utilities. (The name derives from the UNIX *man* [manual] pages.) Perl has divided its *man* pages into categories. If you type the following at your command-line prompt:

```
man perl
```

you will get a list of all the sections by category. So, if you want help on how to use Perl's regular expressions, you would type:

```
man perlre
```

and if you want help on subroutines, you would type:

```
man perlsub
```

The Perl categories are listed in Table 1.2, with the following sections available only in the online reference manual.

**Table 1.2 Perl Categories**

| Category | What It's Used For |
| :--- | :--- |
| *perldb* | Debugging |
| *perldiag* | Diagnostic messages |
| *perldsc* | Data structures: intro |
| *perlmform* | Formats |
| *perlfunc* | Built-in functions |
| *perlloc* | Interprocess communication |
| *perllol* | Data structures: lists of lists |
| *perllmod* | Modules |
| *perlobj* | Objects |
| *perlop* | Operators and precedence |
| *perlpod* | Plain old documentation |
| *perlre* | Regular expressions |
| *perlsoc* | Extensions for socket support |
| *perlstyle* | Style guide |
| *perlsub* | Subroutines |
| *perlintie* | Objects hidden behind simple variables |
| *perltrap* | Traps for the unwary |
| *perlvar* | Predefined variables |

If you are trying to find out how a particular library module works, you can use the *perldoc* command to get the documentation. (This command will give you documentation for the version of Perl you are currently using, whereas the *man* pages refer to the system Perl.) For example, if you want to know about the *Moose* module, type at the command line:

```
perldoc Moose
```

and the documentation for the *Moose.pm* module will be displayed. If you type:

```
perldoc Carp
```

the documentation for the *Carp.pm* module will be displayed.

To get documentation on a specific Perl function, type **perldoc -f** and the name of the function. For example, to find out about the *localtime* function, you would execute the following command at your command-line prompt (you may have to set your UNIX/DOS path to execute this program directly):

```
perldoc -f localtime
```

The output is as follows:

```
localtime EXPR
localtime

Converts a time as returned by the time function to a 9-element list with the time analyzed for the local time zone. Typically used as follows:

#   0   1   2   3   4   5   6   7   8
($sec,$min,$hour,$doy,$mon,$year,$wday,$yday,$isdst) =
    localtime(time);

<continues>
```

### 1.5.3 Online Documentation

ActivePerl provides excellent documentation (from *ActiveState.com*) when you download Perl from its site. As shown in Figure 1.6, there are links to everything you need to know about Perl.

![](img/8556abcb353c0991f12099420ec28735_41_0.png)

Figure 1.6 Perl documentation from ActiveState.
