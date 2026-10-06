
# Advanced Bash–Scripting Guide

```
H --> G
The "SE" diagram falls under case #1.
C O D E S (Row containing "S" and "E")

S --> C (wraps around left to beginning of row)
E --> S
```

To decrypt encrypted text, reverse the above procedure under case #1
and #2 (in opposite direction for substitution). Under case #3,
just taking the two corners of the rectangle.

Helen Fouche Gaines' classic work, "Elementary Cryptanalysis" (1939), gives a
fairly detailed rundown on the Playfair Cipher and its solution methods.

This script will have three main sections:

- I. Generating the "key square", based on a user-input keyword.
- II. Encrypting a "plaintext" message.
- III. Decrypting encrypted text.

The script will make extensive use of arrays and functions.

Please do not send the author your solutions to these exercises. There are better ways to impress him with
your cleverness, as submitting bugfixes and suggestions for improving this book.

# Appendix J. Copyright

The "Advanced Bash–Scripting Guide" is copyright, (c) 2000, by Mendel Cooper. This document may
be distributed subject to the terms and conditions set forth in the LDP License. These are very liberal terms,
and they should not hinder any legitimate distribution or use of this book. The author encourages
the use of this book for instructional purposes.

Essentially, you may freely distribute this book in unaltered electronic form. You must obtain the author’s
permission to distribute a modified version or derivative work. The purpose of this restriction is to preserve
the artistic integrity of this document and prevent "forking".

The commercial rights to this book are available. Please notify the author if interested.

Hyun Jin Cha has done a Korean translation of version 1.0.1 of this book. Spanish, Portuguese, French, and
Chinese translations are underway. If you wish to translate this document into another language, please feel
free to do so, subject to the the terms stated above. The author wishes to be notified of such effects.

Appendix J. Copyright

# Advanced Bash–Scripting Guide

# Notes

- [1] These are referred to as builtins, features internal to the shell.

- [2] Many of the features of ksh88, and even a few from the updated ksh93 have been merged into Bash.

- [3] By convention, user–written shell scripts are Bourne shell compliant generally take a name with a . extension. System scripts, such as those found in /etc/rc.d, do not follow this guideline.

- [4] Some flavors of UNIX (the based on 4.2BSD) take a four-byte magic name, requiring a blank after the !. #! /bin/sh.

- [5] The # line in a shell script will be the first command interpreter (sh or bash) sees. Since this line begins with a #, it will be correctly interpreted as a comment when the command interpreter finally executes the script. The line has already served its purpose – calling the command interpreter.

- [6] This allows some cute tricks.

```bash
#!/bin/rm
# Self-deleting script.

# Nothing much seems to happen when you run this.. except that the file disappears.
WHATEVER=65
echo "This line will never print (betcha!)."

exit $WHATEVER # Doesn't matter. The script will not exit here.
```

Also, trying to script a README file with a #!/bin/more, and making it executable. The result is a self-listing documentation file. (Wait, I missed some text)

- [7] Portable Operating System Interface, an attempt to standardize UNIX–like OSes.

- [8] Caution: invoking a Bash script by sh turns off Bash–specific extensions, and the script may fail to execute.

- [9] A script needs read, as well as execute permission for it to run, since the shell needs to be able to read it.

- [10] Why not simply invoke the script with scriptname? If the directory you are in ($PWD) is where scriptname is located, why does this work? For security reasons, the directory "," is not included in a user’s $PATH. It is therefore necessary to explicitly invoke the script in the current directory with a ./scriptname.

- [11] The shell does the brace expansion. The command itself acts upon the result of the expansion.

- [12] Exception: a code block in braces as part of a pipe may be run as a subshell.

# Appendix J. Copyright

# Advanced Bash–Scripting Guide

```bash
ls | read firstline; read secondline; }
# Error. The code block in braces runs as a subshell,
# so the output of "ls"-cannot be passed to variables within the block.
echo "First line is $firstline; second line is $secondline" # Will not work.
```

# Thanks, S.C.

The process calling sets the $0 parameter. By convention, this parameter is the name of the script. See the mapping of `execv`.

"Word splitting", in this context, dividing a character string into a number of separate and discrete arguments.

Be aware that `suid` binaries may open security holes that the `suid` flag has no effect on shell scripts.

On modern UNIX systems, the sticky bit is not used for files, only on directories.

As S.C. points out, in a compound test, even quoting the...

# Advanced Bash–Scripting Guide

The source for builtins is typically found in /usr/share/doc/bash

Note that the -f option is not portable to all systems.

- [28] The same effect as autoload can be achieved with typeset.

- [29] These are files named with a dot, such as .. Defaults do not show up in a normal listing, and cannot be deleted by rm -rf *.

- [30] A tar cvzf will include directories below the current directory. This is an undocumented feature

- [31] This is a symmetric block cipher, to encrypt files on a single system or local network, as opposed to the "public key" cipher class, pgp is a well-known example.

- [32] A daemon is a background process not attached to a terminal session. Daemons perform designated services either when triggered or explicitly by certain events.

The word "daemon" means ghost in Greek, and there is certainly something mysterious, almost supernatural, about how the UNIX daemons silently wander behind the scenes, carrying out their tasks.

- [33] This is actually a script adapted from the Debian distribution.

- [34] The print queue is the group of jobs "waiting in line" to be printed.

- [35] For an excellent overview of this topic, see Andy Vaught's article, Introduction to Named Pipes, in the September, 1997 issue of Linux Journal.

- [36] EBCDIC (pronounced "ebcd-sid-ic") is an acronym for Extended Binary Coded Interchange Code. It is an IBM data format no longer in use. A application of the conv_ebcdic option of dd is a 'quick' but not very useful text file encoder.

```bash
cat $file dd=swab,ebcdic > $file_encrypted
# Encode (looks like gibberish)
# Might as well switch bytes (swab), too, for a little extra
$file_encrypted dd=swab,ascii > $file_plaintext
# Decode.
```

- [37] A macro is a symbolic constant that expands into a command string or a set of operations on parameters.

- [38] This is the case on a Linux machine or a UNIX system with disk quotas.

- [39] The userdel command will fail if the particular user being deleted is still logged on.

Appendix J. Copyright
