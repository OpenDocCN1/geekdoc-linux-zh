
# SUBSTITUTION MECHANISMS 397

The best way to test the function of special characters is to use the echo command. The first command below supplies all files and directories in the root directory. The second command is a variation in which only names that contain one of the letters a to c are allowed. The third command proves that the generation of file names works across several directory levels. (For reasons of space, the output has been greatly reduced. On my computer, for example, /* works in a list of about 700 files and directories.)

```
user$ echo /*
/CD /bin /cdrom /dev /dist /dosa /dosemu /dosi /etc
/home /install /lib /local /last+found /mnt /proc /root /sbin
/test /tmp /usr /vmlinuz /image
```

```
user$ echo *[a-c]*
/bin /boot /cdrom /dosa /d /etc /install /lib /local /proc
/sbin /var /image
```

```
user$ echo /**
/bin/Mail /bin/arch /bin/bash ....
/boot/any_y.b /boot/any_d.b
/dev/MAKEDEV /dev/arp /dev/bmouseatixl ....
```

Since generation of file names is not carried out by the program in question, but by the bash, results sometimes look different from what you would probably expect. Thus, ls * can lead to a seemingly endless list of files, even though there are only a few files in the current directory. After the expansion of *, ls is a list of all files and directories, however, displays their whole contents. If you just want to have a simple list of all files and directories, you must use the option -d which prevents the contents of the directories specified in the parameter list from being displayed.

If you would like to have feedback on how the bash works internally, you can execute -x. In this case, the bash shows the internal command line (with all options, including those set elsewhere and the expanded file names) before a command is executed.

# Character string generation using braces

The bash combines character strings specified in braces in all possible character combinations. The official term for this substitution mechanism is brace expansion. part(1,2,3) becomes part1 part2 part3. Brace expansion can reduce the amount of typing required for accessing similar file or directory names. Unlike wildcards, as * and ?, the answer is even non-existent file names can be generated (for example, for use with mkdir).

# THE BASH - A MODERN COMMAND INTERPRETER

```
user echo {a,b}{1,2,3}
a1 a2 a3 b1 b2 b3
```

```
user echo {a,b,c}{e,f,g}{1,2,3}
ae.1 ae.2 ae.3 af.1 af.2 af.3 ag.1 ag.2 ag.3 be.1 be.2 be.3
bf.1 bf.2 bf.3 bg.1 bg.2 bg.3 ce.1 ce.2 ce.3 cf.1 cf.2 cf.3
cg.1 cg.2 cg.3
```

# Calculation of arithmetic expressions in square brackets

Normally, the bash is not capable of executing calculations. The shell does not know what to do with this expression. If you want to carry out a calculation within the shell, you must enclose the expression in square brackets and precede it with a $ sign.

```
user echo ${2+3}
```

5 Inside the square brackets, most operators of the C programming language are allowed: - * / for the four fundamental operations, % for modulo calculations, != < and > for comparisons, << and >> for shift operations, && || for logical NOT, AND, and OR. All calculations are executed as 32-bit integer numbers (value range between ±2 and 147 483 648). If values have to be extracted from variables, they must be preceded by a $ sign (see page 400 about variable management).

An alternative way to execute calculations is provided by the expr command. This is an autonomous Linux command which works independently of the bash (see page 453).

# Command substitution

Command substitution allows you to substitute a command in the command line with its result. For this purpose, the command must be enclosed in two ' characters, or as $(command). This latter notation is preferable: it reduces the confusion caused by three kinds of quotes (", '\', '\') and it can be embedded.

However it is written, the command is substituted with its result. This substitution allows embedded calls to several commands, where one command passes the result to the next command. The following example illustrates this very powerful mechanism:

```
ls -l 'find /usr/doc -name *README*'
ls -l $(find /usr/doc -name *README*) #
With the above command, first find /usr/doc -name *README*' is executed.
```

The result of this command is a list of all files in the /usr/doc directory in which the character 'README' occurs. This list is now inserted into the command line in place of the find command. Now, the command line might look like this:

# SUBSTITUTION MECHANISMS 399

```
user$ ls -l /usr/doc/xpm33/README /usr/doc/term/README.gz \
> /usr/doc/mt-st/README /usr/doc/README.gz
 (only internally combined) command supplies the following:
-rw-r--r 1 root 1854 Apr 24 22:49 /usr/doc/README.gz
-rw-r--r 1 root 847 Sep 21 1993 /usr/doc/mt-st/README
-rw-r--r 1 root 5796 Apr 20 1994 /usr/doc/term/README.gz
-rw-rw--r-- 1 root 5550 Jan 30 1994 /usr/doc/xpm33/README
```

Please note that the same result could not have been obtained by a simple pipe using the | character. It does not expect input from the standard input and ignores the information supplied by find through the pipe. Consequently the following command just displays the contents of the current directory. The results of find are not displayed!

```
user$ find /usr/doc -name 'README' | ls -l # this does not work
```

There is, another solution that does not require command substitution: by means of the command xargs data is redirected from the standard input to the command specified after xargs.

```
user$ find /usr/doc -name 'README' | xargs ls -l
```

# Special characters in character strings

In the bash practically every character, with the exception of letters and numbers, appears to have some special meaning, it seems to be quite impossible to use these characters in strings or file names. This problem can be solved in two ways. Either the special character is preceded by a backslash or the character is enclosed in single or double quotes. With the use of quotes, you can, for example, delete a file with the name ab*Scd:

```
user$ rm 'ab*Scd'
```

Please note the difference between (for character identification) and (for command substitution, see above). Double quotes have a similar effect to single quotes, but they are less restrictive and allow the interpretation of a few special characters ($, \). Thus in strings placed within double quotes, shell variables with a prefixed $ sign will be evaluated.

```
user$ echo "This is the access path: PATH"
```

As a result the command supplies the character string 'This is the access path', followed by the contents of the shell variable PATH. If single quotes are used instead of double ones, echo outputs the whole character string unchanged. More information about shell variables is given in the next section.

- A summary of all bash special characters can be found at the end of Chapter 13, on page 435.

![](img/b30873dd3d753687a59253fb9ad26a0b_426_0.png)

# Syntax summary

Substitution mechanisms
Wildcards for file names

| | | |
|---|---|---|
| `*` | exactly one arbitrary character | any number (including zero) arbitrary characters (but no . * files!) |
| `[abc]` | one of the specified characters | |
| `[a-f]` | one character out of the specified range | |
| `[!abc]` | none of the specified characters | |
| `[^abc]` | same as above abbreviation for the home directory |
| `..` | current directory next higher directory |

Character string combinations
ab(1,2,3) yields ab1 ab2 ab3

Arithmetics
$[3*4] arithmetic calculations

Command substitution
`command` substitutes the command with its result
$(command)` same as above, alternative notation

Evaluation of "character" strings
command `character'` prevents evaluation of special characters
command `character'` same as above, but more restrictive

# 12.6 Shell variables

The functionality of the bash and many other Linux programs is controlled by the state of socalled shell variables. Shell variables are comparable to programming language variables, with the difference that they can only store character strings (no numbers). The assignment of shell variables is carried out by means of the operator =. The easiest way to display the contents of a shell variable is to use echo with the variable name preceded by a $ sign.

```
user var=abc
user echo $var
ab
```

If the contents of a shell variable are to contain spaces or other special characters, then the whole character string must be enclosed in single or double quotes in the assignment operation.
