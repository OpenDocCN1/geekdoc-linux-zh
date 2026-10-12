```
config.guess   install-sh   sudo.man
config.h       insults.h    sudo.o
```

This is a directory listing of the source code and object code generated for the sudo command. With this directory listing as our sample, we will answer the following questions using the echo and ls commands to generate the desired output.

+   1. Which of these files begin with the letter "I"?
+   2. Which files in the directory contain the character "y"?
+   3. How would you assign all filenames that end in ".c" or ".h" to a shell variable FOO?
+   4. How would you copy all files starting with "y." to your home directory?
+   5. How would you list all files starting with "visudo." except those ending with a ".c" or ".o" extension?
+   6. How can you list all files starting with the letter "s" and ending with a single character extension?

The first question asks us to list all files beginning with the letter "I". This example will demonstrate the use of the "*" globbing character. To answer this question, we would issue the following command, giving the output shown.

```
[tschenk@quicksilver sudo.v1.5.3]$ ls I*
INSTALL
INSTALL.configure
```

The next question also requires the use of the "*" globbing character. Remember that this character matches zero or more characters, thus the expression "*y*" used in the following command translates to "zero or more characters followed by the letter 'y' followed by zero or more characters." This means that the output will include files that start and end with the letter "y" as well as those that include "y" somewhere in the middle. Here is the command and its output:

```
[tschenk@quicksilver sudo.v1.5.3]$ ls *y*
sixcrypt.exp  lex.yy.o  sudo-lex.yy.c  y.tab.h
lex.yy.c      parse.yacc  y.tab.c  y.tab.o
```

In the next example, we will use the echo command to assign all of the files ending with ".c" or ".h" to a shell environment variable FOO. This will demonstrate the use of the brackets in filename substitution.

```
[tschenk@quicksilver sudo.v1.5.3]$ FOO=`echo *.[ch]`
[tschenk@quicksilver sudo.v1.5.3]$ echo $FOO
allocca.c check.c compat.h config.h doe_pwent.c find_path.c fnmatch.c
getspuid.c getwd.c goodpath.c ins_2001.h ins_classic.h ins_csops.h
ins_goons.h insults.h interfaces.c lex.yy.c logging.c lsearch.c options.h
parse.c pathnames.h putenv.c strdup.c sudo-lex.yy.c sudo.c sudo.h
```