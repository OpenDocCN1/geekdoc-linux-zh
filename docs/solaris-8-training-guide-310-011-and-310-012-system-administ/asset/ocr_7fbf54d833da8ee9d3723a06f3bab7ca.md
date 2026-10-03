located in /etc/init.d) and most third-party software are also written in the Bourne shell. In addition, because the Bourne shell is located in /sbin, it’s the only shell available when /usr is not mounted (that is, in single-user mode). The Bourne shell was designed from the beginning for use as a programming language, which explains its breadth of programming features. An additional reason for using the Bourne shell is that its conditionals and controls are compatible with all other shells, including the dt ksh shell used in the CDE environment. dt ksh is discussed in Appendix B.

All examples in this chapter use the Bourne shell.

# BOURNE SHELL VARIABLES

A variable is a name that refers to a temporary storage area in memory. A value such as a text string or number is assigned to a variable and can be changed at any time. The Bourne shell uses two types of variables to store values: local and environmental. Each is described in this chapter.

A variable is either set to some particular value or is said to be “unset,” which means that it does not exist as a variable. Shell variables are an integral part of shell programming. The shell variable provides the capability to store and manipulate information within a shell program. The variables you use are completely under your control, and you can set or unset any number of variables as needed to perform a particular task.

A variable name must begin with a letter, and can contain letters, digits, and underscores, but no special characters. In the Bourne shell, environment variables are set with an assignment of NAME=value. In the following example, the ME and BC variables are set by entering the following at a command prompt:

```
ME=bill
BC="bill calkins"
```

Be sure not to have any white space before or after the equals sign (=). Double quotes, as used in the second example, are used when white space is present in the text string you are assigning to the variable. Whenever the shell sees a $variable, such as $ME, it substitutes into the command line the value stored for that variable.