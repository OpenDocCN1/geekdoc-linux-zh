
## Table 2.1 Regular Expression Meta Characters

| Meta Character | Meaning |
|---|---|
| . | Match any single character. |
| + | Match the previous character 1 or more times. |
| * | Match the previous character 0 or more times. |
| ? | Match the previous character 0 or 1 times. |
| ^ | Start matching at the beginning of a string. |
| $ | Match the end of a string. |
| | | The OR operator. |

By using these wildcards along with some strings, you can construct some simple regular expressions. To demonstrate the use of regular expressions, we will start with a file containing the following lines:

```
tschenk:x:500:100:Thomas Schenk,Rm 164,502-2663,:/home/tschenk:/bin/bash
eunjoung:x:501:100:E.J. Schenk,Rm 503,503-1467,:/home/eunjoung:/bin/bash
nicholas:x:502:100:Nick Schenk,Rm 503,503-1465,:/home/nicholas:/bin/tcsh
nia:x:503:105:Nia Schenk,Rm 104,502-6514,:/home/nia:/bin/bash
bob:x:504:105:Robert Smith,Rm 504,503-1465,:/home/bob:/bin/ksh
bkreed:x:505:100:Bob Reed,Rm 504,503-1467,:/home/bkreed:/bin/bash
chuck:x:506:100:Charles Brown,Rm 104,502-4158,:/home/chuck:/bin/bash
chucky:x:507:105:Chuck Jones,Rm 564,503-1465,:/home/chucky:/bin/zsh
diane:x:508:100:Diane Wilson,Rm 104,502-4156,:/home/diane:/bin/bash
dwilson:x:509:100:Dwight Wilson,Rm 504,503-1466,:/home/dwilson:/bin/tcsh
ashley:x:510:105:Ashley Waters,Rm 504,503-1468,:/home/ashley:/bin/tcsh
bashton:x:511:100:Bill Ashton,Rm 100,502-6105,:/home/bashton:/bin/zsh
```

As you can see, this is part of a password file and for the purposes of our examples, we will refer to it as passwd. Using this file, we will attempt to use egrep with some simple regular expressions to find the answers to the following questions:

- 1. How many users in the passwd file have a last name of Schenk?
- 2. How many users have a first name of Bob or Robert?
- 3. What is the full name of the user chuck?
- 4. How many users use bash as their shell?

To answer the first question, we need to know the structure of the passwd file. In the passwd file, the last name is preceded by a space and followed by a comma. With this knowledge, we could issue the following command to find out how many people in the passwd file have a last name of Schenk.

```
egrep " Schenk," passwd
```

It could be argued that in this case, the comma and the space were not required to get the correct answer. However, it is good practice to describe the string you are searching for as much as possible. The regular expression as shown contains no special characters. It consists of a simple string of characters. The meaning of this regular expression is “a space followed by the word Schenk followed by a comma.” Here is the output of the command as you would see it on the command line:

```
tschenk:x:500:100:Thomas Schenk,Rm 164,502-2663,:/home/tschenk:/bin/bash
eunjoung:x:501:100:E.J. Schenk,Rm 503,503-1467,:/home/eunjoung:/bin/bash
nicholas:x:502:100:Nick Schenk,Rm 503,503-1465,:/home/nicholas:/bin/tcsh
nia:x:503:105:Nia Schenk,Rm 104,502-6514,:/home/nia:/bin/bash
```

How many users have a first name of Bob or Robert? This second question is similar to the first. To answer this question, we could issue the following egrep command, which demonstrates the use of the | operator in a regular expression. The | is an OR operator and is used to specify that you are searching for either the string on the left-hand side of the | symbol or the string on the right-hand side. It also demonstrates one of the uses of parentheses in regular expressions.

```
egrep ':(Bob|Robert) ' passwd
```

In this example, the regular expressions could be translated as “a colon, followed by either the string Bob or the string Robert, followed by a space.” Note the parentheses surrounding the strings Bob and Robert. These are examples of the grouping operators. The output of this command would look like this:

```
bob:x:504:105:Robert Smith,Rm 504,503-1465,:/home/bob:/bin/ksh
bkreed:x:505:100:Bob Reed,Rm 504,503-1467,:/home/bkreed:/bin/bash
```

Our third question is, “What is the full name of the user chuck?” This requires use of one of the positional meta characters to get the single line containing the correct answer. It also requires that you know the format of the passwd file. Failure to take into account the structure of the passwd file could lead you to issue the following command:

```
egrep 'chuck' passwd
```

This would result in the following output, which contains the correct line as well as an incorrect line for a user with an id of chucky. In addition, if the passwd file contained a user id of upchuck or woodchuck, these would also have been returned.

```
chuck:x:506:100:Charles Brown,Rm 104,502-4158,:/home/chuck:/bin/bash
chucky:x:507:105:Chuck Jones,Rm 504,503-1465,:/home/chucky:/bin/zsh
```

The most correct regular expression to use to answer this question would specify that the matching line begin with the string chuck followed by a colon. The egrep command using this regular expression would be as shown here:

```
egrep "^chuck:" passwd
```

This command would return the single line that begins with the word chuck followed by a colon and give us the answer to the third question: Charles Brown.

The final question, "How many users use bash as their shell?", requires the use of another of the positional meta characters to avoid getting extra data. At first glance, it would appear that a simple command such as the following would give the correct answer:

```
egrep "bash" passwd | wc -l
```

This would result in an answer of six, which is incorrect due to the inclusion of the userid bashton in the results. Again, knowledge of the structure of the passwd file is required to formulate the correct regular expression, demonstrated in this command, which returns the correct answer of five:

```
egrep "bash$" passwd | wc -l
```

In addition to the regular expression meta characters shown here, there are others that include ways to specify a range or set of characters, referred to as bracket expressions. Table 2.2 shows examples of bracket expressions and their meanings.

## TABLE 2.2 Bracket Expressions

| Regular Expression | Meaning |
|---|---|
| [A-Z] | Match all characters in the range A-Z in the current character set collating sequence. |
| [13579] | Match all characters specified between the brackets. |
| [^a-z] | Match all characters not in the range a-z in the current character set collating sequence. |
| [:alpha:] | Match all characters in the alpha class as defined in ctype(3). |
| [*?+|] | Match the characters "*", "?", "+", "|". |

There are forms of regular expressions other than those covered here, but a full discussion of them is beyond the scope of this book. Many of the commands in the power user arsenal rely on knowledge of regular expressions, as do scripting languages like perl and tcl.

## Filename Substitution

Filename substitution, or globbing, confuses many users because it uses many of the same meta characters as regular expressions, but they have different meanings. Table 2.3 shows the common globbing characters and their meanings. These apply to both the Bourne Again Shell (bash) and tcsh, an enhanced version of the Berkeley C-shell, the two most popular shells on Linux systems.

### TABLE 2.3 Filename Substitution Meta Characters

| Globbing Character | Meaning |
|---|---|
| ? | Match any single character in a filename. |
| * | Match zero or more characters in a filename. |
| [...] | Match any of the characters between the brackets. |
| [^...] | Match any characters not specified in the brackets. |
| {aaa,bbb,ccc} | Expand to aaa, bbb, and ccc in order. |
| ~ | Expand to the current user's home directory if it is the first character in the pattern. |

To better understand this concept of filename substitution, we will assume the following directory contents and demonstrate using various shell commands, such as ls and echo.

```
BUGS               config.h.in      interfaces.c      sudo.pod
CHANGES            config.log        interfaces.o      sudo_setenv.c
COPYING            config.status     lex.yy.c          sudo_setenv.o
FAQ                config.sub        lex.yy.o          sudoers
HISTORY            configure         logging.c         sudoers.cat
INSTALL            configure.in      logging.o         sudoers.man
INSTALL.configure  dce_pwcnt.c       lsearch.c         sudoers.pod
Makefile           emul              mkinstalldirs     testsudoers.c
Makefile.in        find_path.c       options.h         tgetpass.c
OPTIONS            find_path.o       parse.c           tgetpass.o
PORTING            fmmatch.3         parse.lex         utime.c
README             fmmatch.c         parse.o           version.h
RUNSON             getspuid.c        pathnames.h       visudo*
TODO               getspuid.o        parse.yacc        visudo.c
TROUBLESHOOTING    getwd.c           putenv.c          visudo.cat
acsite.m4          goodpath.c        sample.sudoers    visudo.man
aixcrypt.exp       goodpath.o        strdup.c          visudo.o
aloca.c            indent.pro        sudo              visudo.pod
check.c            ins_2001.h        sudo-lex.yy.c     y.tab.c
check.o            ins_classic.h     sudo.c            y.tab.h
compat.h           ins_csops.h       sudo.h            y.tab.o
config.cache       ins_goons.h       sudo.h
```
