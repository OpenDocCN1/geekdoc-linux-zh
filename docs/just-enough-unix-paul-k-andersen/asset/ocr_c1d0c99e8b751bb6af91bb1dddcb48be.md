```
(ksh)

alias rm='rm -i'
```

Alternatively, you could put the following line in your `.profile`, using the `-x` option to export the command to all subshells:

```
alias -x rm='rm -i'
```

The `-x` option exports the alias (ksh).

# 20.13 **Comment Lines**

A *comment* is text in a startup file (or a program) that is ignored by the shell when the file is executed. Comments are useful for reminding you of the file's purpose. In shell startup files, a comment begins with a pound sign (#). For example,

```
# This is a comment line
```

# 20.14 **Exercises**

+   1. Be sure you can define the following terms:
+       
+       startup file 
+       
+       login initialization file 
+       
+       shell initialization file 
+       
+       subshell 
+       
+       variable 
+       
+       special shell variable 
+       
+       environment variable 
+       
+       alias

+   2. Be sure you can explain the function or contents of each of the following files:
+       
+       .cshrc 
+       
+       .exrc 
+       
+       .forward 
+       
+       .kshrc 
+       
+       .login 
+       
+       .logout 
+       
+       .mailrc 
+       
+       .mmwrc 
+       
+       .newsrc 
+       
+       .plan 
+       
+       .profile 
+       
+       .xinitrc

+   3. Be sure you can explain the purpose of each of the following variables:
+       
+       HOME 
+       
+       MAIL 
+       
+       PATH 
+       
+       PWD 
+       
+       SHELL 
+       
+       TERM

+   4. Suppose a sh user wanted to create a variable named *myhome* to hold the path-name of his or her home directory.
+       
+   a. What command(s) should be put in the login initialization file so that *myhome* will be usable by the login shell only?
+       
+   b. What command(s) will ensure that *myhome* will be available to all sub-shells? (The variable HOME contains the pathname of the home directory.)

+   5. Repeat the previous problem, assuming that ksh is the login shell.

+   6. Repeat the previous problem, assuming that csh is the login shell.