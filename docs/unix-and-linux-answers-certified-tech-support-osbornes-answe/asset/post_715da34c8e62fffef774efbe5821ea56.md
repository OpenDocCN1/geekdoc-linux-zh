
# Can I use tar to back up my files to a floppy or tape drive?

If you have a floppy drive in your workstation, you probably already know what the device file name for it is, but if in doubt, ask your system administrator and then write it down where you won’t lose it. One possible place is right on the front of the floppy drive in permanent marker. A typical device might be /dev/fd0 for the first floppy, so the tar command to save your entire home directory and all the files in it would be

```
tar cvf /dev/fd0 $HOME
```

If you want to save the files with relative path names, not the absolute ones that this would give you, change to your home directory first, substitute a simple dot for the $HOME, and you’re in business.

## Chapter 13

## The Korn Shell

## Answer Topics!

- **VARIABLES AND PARAMETERS 198**
  - How the Korn shell uses variables and parameters
  - Assigning values to a variable
  - The Korn shell and the Posix shell
- **KORN SHELL MATH 199**
  - How the Korn shell does math
- **STRING OPERATORS 202**
  - Concatenating strings in the Korn shell
  - String substitution operators
- **PREDEFINED VARIABLES IN THE KORN SHELL 204**
  - Redefining a predefined variable
- **FLOW CONTROL 205**
  - Flow control structures in the Korn shell
  - Using if/then/else statements in the Korn shell
  - Using for loops in the Korn shell
  - Using while and until loops in the Korn shell
  - Using case statements
  - Using the select statement

## The Korn Shell @ a Glance

**Variables and parameters** are an important part of any programming language, and the Korn shell is no exception. Here we'll show you what you need to know in order to use them intelligently.

In case you get confused, it's nice to know ahead of time exactly how the **Korn shell** does **math**.

Although the Korn shell's math capabilities are somewhat limited, its capabilities with **string operators** are impressive, as you'll soon see.

You'll save yourself some trouble if you are aware of the **predefined variables** that the Korn shell offers you.

Finally, **flow control** is one of the most important capabilities of any programming language or environment. The Korn shell provides a wide array of flow control structures, so here's what you'll need to know in order to make the best possible use of them.

## VARIABLES AND PARAMETERS

### What kind of use does the Korn shell make of variables and parameters?

Like any programming tool, the Korn shell lets you define variables and accepts input parameters. Parameters are anything that appears on the command line (or is piped into the command) after the command itself. The Korn shell separates or parses these parameters by looking for white space in between them, or, more properly, whatever characters are in the IFS (internal field separator) variable. By default, this is space, tab, and newline, but you can change this to make it easier to parse a set of options. But be sure to set it back when you get done. The positional parameters are automatically assigned by the shell as $1, $2, $3, and so forth. The value of $0 is the name of the calling script. The variable $* holds all the values except $0, as a single string within which each value is separated by the first character of $IFS. The variable $# is equal to "$1", "$2", and so forth as separate parameters.

### How do I assign values to a variable?

Use the syntax

```
variable=value
```

For example, the following

```
wayne=harold
print "Wayne is now called $wayne"
```

results in

```
Wayne is now called harold
```

## The Korn Shell and the POSIX Shell

The Korn shell was invented by David Korn in the 1980s at AT&T’s Bell Labs. It’s gone through several iterations, but the one most commonly available was written in 1988 and has been distributed on a wide range of UNIX platforms since that time—especially those known as System V Release 4 (SVR4)—though most flavors of UNIX based on the Berkeley System Distribution (BSD) also now support the Korn shell. The Korn shell continues to be developed, and new versions are likely to see the light of day over time. The Posix shell, however, seems to be replacing the Korn shell in many instances. Most of the features of the Korn shell have found their way into the common implementations of the Posix shell, and your Korn shell scripts should port to Posix shell with little or no changes.

Most of the examples we have used in this book have been written and tested under the Korn shell, and by this point in the book you’ve probably picked up quite a few things about it. But we felt that it would be useful to give you a reference for some of the basics of shell programming, as opposed to interactive use, that the Korn shell supports in a form less dense than the man pages.

## KORN SHELL MATH

### Is there anything in particular I should know about the way the Korn shell does math?

You can do simple math within a Korn shell script, though if you want to do much of it, there are far better choices for programming languages than the Korn shell. But, for example, you can declare a variable, i, and assign a value to it in one of the following ways:
