The sendmail-cf package installs in the /usr/share/sendmail-cf directory all the files needed to generate a new sendmail.cf configuration file. As I explain in the next few sections, the sendmail.cf file is generated from a number of m4 macro files (text files in which each line eventually expands to multiple lines that mean something to some program). These macro files are organized into a number of subdirectories under /usr/share/sendmail-cf. You can read the README file in /usr/share/sendmail-cf to learn more about the creation of sendmail configuration files.

Now that you've taken care of the prerequisites, you can learn how to regenerate the sendmail.cf file.

# m4 macro processor

The m4 macro processor is used to generate the sendmail.cf configuration file, which comes with the sendmail package in Red Hat Linux. The main macro file, sendmail.mc, is included with the sendmail package, but that file needs other m4 macro files that are in the sendmail-cf package.

So what's a macro? A macro is basically a symbolic name for code that handles some action, usually in a shorthand form that substitutes for a long string of characters. A macro processor such as m4 usually reads its input file and copies it to the output, processing the macros along the way. The processing of a macro generally involves performing some action and generating some output. Because a macro generates a lot more text in the output than merely the macro's name, the processing of macros is referred to as macro expansion.

The m4 macro processor is stream-based. That means it copies the input characters to the output while it's busy expanding any macros. The m4 macro processor does not have any concept of lines, so it copies newline characters (that mark the end of a line) to the output. That's why you see the word dn1 in most m4 macro files; dn1 is an m4 macro that stands for "delete through newline." The dn1 macro deletes all characters starting at the dn1 up to and including the next newline character. The newline characters in the output don't cause any harm; they merely create unnecessary blank lines. The sendmail macro package uses dn1 to avoid such blank lines in the output configuration file. Because dn1 basically means delete everything up to the end of the line, m4 macro files also use dn1 as the prefix for comment lines.

To see a very simple use of m4, consider the following m4 macro file that defines two macros — hello and bye — and uses them in a form letter:

```
dn1 ##################################################
dn1 # File: ex.m4
dn1 # A simple exampls of m4 macros
dn1 ##################################################
define(`hello', `Dear Sir/Madam')dn1
```

![](bbox=[0.14, 0.5, 0.22, 0.66])