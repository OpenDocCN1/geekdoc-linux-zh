
## OTHER TOOLS THAT ARE DIFFERENT UNDER LINUX

Figure 14-2 A clean and elegant shell prompt

What are some tools that might be different under Linux?

Other things you might encounter that are different from more conventional UNIX tools include, but aren't limited to:

- less A better pager than the standard more.
- gzip Better compression than the standard compress.
- crypt Usually not available, due to U.S. export restrictions. There are replacements available, though, which aren't subject to U.S. export control laws.
- ispell An internationalized version of the standard spell utility.
- ncftp A friendlier and more versatile command-line ftp client.
- gcc/g++ C/C++ compilers, usually an expensive added option for commercial UNIX boxes.

![](img/0c1fc10350aa06ca92e7921c96c628ec_266_0.png)

## Chapter 14  Linux

| 命令 | 说明 |
|---|---|
| `control-panel` | A graphical system management tool that is comparable to or better than nearly every commercial vendor's offering. |
| `ghostview` | Displays postscript files. |
| `gv` | Also displays postscript files, in addition to Adobe acrobat (.PDF) files. Sort of a ghostview on steroids. |
| `samba` | Allows you to share resources to and from Microsoft Windows machines. |

## Chapter 15

## awk, perl, and sed

## Answer Topics!

- THE AWK PROGRAMMING LANGUAGE 239
  - awk is the product of three familiar UNIX names
  - How to call awk and use its options
  - Example of how to use awk
- THE PERL PROGRAMMING LANGUAGE 242
  - perl is an eclectic gem
- THE SED PROGRAMMING LANGUAGE 245
  - Automating is easier
  - What sed is
  - Why use sed
  - How sed works
  - Examples of how to use sed
- Differences between awk and perl

## awk, perl, and sed @ a Glance

In addition to a full-service toolbox, UNIX offers three programming languages intended to help you expand your toolbox to suit your particular needs. awk is a pattern-matching language that can be used for simple tasks or for complex text manipulations.

perl is another pattern-matching language that may suit some of you better than awk, but this depends on your needs and inclinations.

Finally, sed is a command-line, streaming editor that lets you feed a text file through it so that you can change a file entirely from within a script.

## awk Is the Product of Three Familiar UNIX Names

awk is named for its three codevelopers, Alfred Aho, Peter Weinberger, and Brian Kernighan. It's available as part of the standard UNIX distribution in its original form at least and usually also in a later version written in 1985 by the original authors called "new awk" or nawk. If you get serious about awk, you'll want to make sure your system has the nawk version, or you can obtain the GNU version, gawk, which adds most of the same enhancements to the original that nawk did. We'll use awk for this discussion.

## How can I call awk and what are some of the options it offers me?

The awk program is called with the command-line syntax:

```
awk [option] [script] [file]
```

The most common option is -f scriptfile, which reads in the script from a file instead of on the command line. An awk program consists of the form:

```
pattern {action}
```

where either the pattern-matching part or the action part is optional. If no pattern is specified, the action is performed on every line of the input; if no action is specified, the default action of { print $0 } is performed on each line that matches the pattern. Since "$0" is a special parameter whose value is the entire line of input, the result is that the default action is to print the line that matches the input. This leads to one obvious use of awk as a somewhat more sophisticated version of grep. For example, the following will look for every line in a file that begins with a number and print out the entire line.

```
awk '/^[0-9]/' filename
```
