
In 1990 Standard C, code written in the original style, for both declarations and definitions, is valid. This makes it possible to continue to compile millions of lines of existing code with a standard-conforming compiler. New code, obviously, should be written with prototypes because of the improved possibilities for compile-time error checking.

1999 Standard C continues to allow original style declarations and definitions. However, the “implicit int” rule was removed; functions must have a return type, and all parameters must be declared.

Furthermore, when a program called a function that had not been formally declared, Original C would create an implicit declaration for the function, giving it a return type of `int`. 1990 Standard C did the same, additionally noting that it had no information about the parameters. 1999 Standard C no longer provides this “auto-declare” feature.

Other notable additions in Standard C are the `const` keyword, also from C++, and the `volatile` keyword, which the committee invented. For the code you’ll see in this book, understanding the different function declaration and definition syntaxes is the most important thing.

For V7 code using original style definitions, we have added comments showing the equivalent prototype. Otherwise, we have left the code alone, preferring to show it exactly as it was originally written and as you’ll see it if you download the code yourself.

Although 1999 C adds some additional keywords and features beyond the 1990 version, we have chosen to stick to the 1990 dialect, since C99 compilers are not yet commonplace. Practically speaking, this doesn’t matter: C89 code should compile and run without change when a C99 compiler is used, and the new C99 features don’t affect our discussion or use of the fundamental Linux/Unix APIs.

## 1.4 Why GNU Programs Are Better

What is it that makes a GNU program a GNU program?⁶ What makes GNU software “better” than other (free or non-free) software? The most obvious difference is the GNU General Public License (GPL), which describes the distribution terms for GNU software. But this is usually not the reason you hear people saying “Get the GNU version of xyz, it’s much better.” GNU software is generally more robust, and performs better, than standard Unix versions. In this section we look at some of the reasons why, and at the document that describes the principles of GNU software design.

The *GNU Coding Standards* describes how to write software for the GNU project. It covers a range of topics. You can read the *GNU Coding Standards* online at http://www.gnu.org/prep/standards.html. See the online version for pointers to the source files in other formats.

In this section, we describe only those parts of the *GNU Coding Standards* that relate to program design and implementation.

### 1.4.1 Program Design

Chapter 3 of the *GNU Coding Standards* provides general advice about program design. The four main issues are compatibility (with standards and Unix), the language to write in, reliance on nonstandard features of other programs (in a word, “none”), and the meaning of “portability.”

Compatibility with Standard C and POSIX, and to a lesser extent, with Berkeley Unix is an important goal. But it’s not an overriding one. The general idea is to provide all necessary functionality, with command-line switches to provide a strict ISO or POSIX mode.

C is the preferred language for writing GNU software since it is the most commonly available language. In the Unix world, Standard C is now common, but if you can easily support Original C, you should do so. Although the coding standards prefer C over C++, C++ is now commonplace too. One widely used GNU package written in C++ is groff (GNU troff). With GCC supporting C++, it has been our experience that installing groff is not difficult.

The standards state that portability is a bit of a red herring. GNU utilities are ultimately intended to run on the GNU kernel with the GNU C Library.⁷ But since the kernel isn’t finished yet and users are using GNU tools on non-GNU systems, portability is desirable, just not paramount. The standard recommends using Autoconf for achieving portability among different Unix systems.

7 This statement refers to the HURD kernel, which is still under development (as of early 2004). GCC and GNU C Library (GLIBC) development take place mostly on Linux-based systems today.

### 1.4.2 Program Behavior

Chapter 4 of the GNU Coding Standards provides general advice about program behavior. We will return to look at one of its sections in detail, below. The chapter focuses on program design, formatting error messages, writing libraries (by making them reentrant), and standards for the command-line interface.

Error message formatting is important since several tools, notably Emacs, use the error messages to help you go straight to the point in the source file or data file at which an error occurred.

GNU utilities should use a function named `getopt_long()` for processing the command line. This function provides command-line option parsing for both traditional Unix-style options (`gawk -F: ...`) and GNU-style long options (`gawk --field-separator=: ...`). All programs should provide `--help` and `--version` options, and when a long name is used in one program, it should be used the same way in other GNU programs. To this end, there is a rather exhaustive list of long options used by current GNU programs.

As a simple yet obvious example, `--verbose` is spelled exactly the same way in `all` GNU programs. Contrast this to `-v`, `-V`, `-d`, etc., in many Unix programs. Most of Chapter 2, "Arguments, Options, and the Environment," page 23, is devoted to the mechanics of argument and option parsing.

### 1.4.3 C Code Programming

The most substantive part of the GNU Coding Standards is Chapter 5, which describes how to write C code, covering things like formatting the code, correct use of comments, using C cleanly, naming your functions and variables, and declaring, or not declaring, standard system functions that you wish to use.

Code formatting is a religious issue; many people have different styles that they prefer. We personally don't like the FSF's style, and if you look at `gawk`, which we maintain, you'll see it's formatted in standard K&R style (the code layout style used in both editions of the Kernighan and Ritchie book). But this is the only variation in `gawk` from this part of the coding standards.

Nevertheless, even though we don't like the FSF's style, we feel that when modifying some other program, sticking to the coding style already used is of the utmost importance. Having a consistent coding style is more important than which coding style you pick. The *GNU Coding Standards* also makes this point. (Sometimes, there is no detectable consistent coding style, in which case the program is probably overdue for a trip through either GNU `indent` or Unix `scb`.)

What we find important about the chapter on C coding is that the advice is good for any C coding, not just if you happen to be working on a GNU program. So, if you're just learning C or even if you've been working in C (or C++) for a while, we recommend this chapter to you since it encapsulates many years of experience.

### 1.4.4 Things That Make a GNU Program Better

We now examine the section titled *Writing Robust Programs* in Chapter 4, *Program Behavior for All Programs*, of the *GNU Coding Standards*. This section provides the principles of software design that make GNU programs better than their Unix counterparts. We quote selected parts of the chapter, with some examples of cases in which these principles have paid off.

- Avoid arbitrary limits on the length or number of any data structure, including file names, lines, files, and symbols, by allocating all data structures dynamically. In most Unix utilities, "long lines are silently truncated." This is not acceptable in a GNU utility.

This rule is perhaps the single most important rule in GNU software design—*no arbitrary limits*. All GNU utilities should be able to manage arbitrary amounts of data.

While this requirement perhaps makes it harder for the programmer, it makes things much better for the user. At one point, we had a *gawk* user who regularly ran an *awk* program on more than 650,000 files (no, that's not a typo) to gather statistics. *gawk* would grow to over 192 megabytes of data space, and the program ran for around seven CPU hours. He would not have been able to run his program using another *awk* implementation.¹

- Utilities reading files should not drop NUL characters, or any other nonprinting characters *including those with codes above* `0177`. The only sensible exceptions would be utilities specifically intended to interface to certain types of terminals or printers that can't handle those characters.
