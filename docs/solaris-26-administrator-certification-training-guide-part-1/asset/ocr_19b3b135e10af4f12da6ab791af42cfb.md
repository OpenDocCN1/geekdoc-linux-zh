we've used it for so many years. On the other hand, I find that SystemV users prefer the Korn shell. These preferences stem back to the early development days of UNIX and are discussed in Appendix A. “The History of UNIX.” For system administration, the Bourne shell is best for writing your scripts. The Bourne shell is the default shell in Solaris and is the only shell found on all UNIX systems. The Bourne shell was designed from the beginning for use as a programming language, which explains its breadth of programming features. An additional reason for using the Bourne shell is that its conditionals and controls are compatible with all other shells, including the dt*ksh shell used in the CDE environment and discussed in Chapter 7, “Administration and Configuration of the CDE.” All examples used in this chapter will use the Bourne shell.

# Bourne Shell Variables

A variable is a name that refers to a temporary storage area in memory. A value such as a text string or number is assigned to a variable and can be changed at any time. The Bourne shell uses two types of variables to store values: local and environmental. Each is described in this chapter.

A variable is either set to some particular value or is said to be “unset,” which means it does not exist as a variable. Shell variables are an integral part of shell programming. The shell variable provides the capability to store and manipulate information within a shell program. The variables you use are completely under your control, and you can set or unset any number of variables as needed to perform a particular task.

A variable name must begin with a letter and may contain letters, digits, and underscores but no special characters. In the Bourne shell, environment variables are set with an assignment of NAME=value. In the following examples, the ME and BC variables are set by entering the following at a command prompt:

```
ME=bill
BC="bill calkins"
```

Be sure not to have any white space before or after the equals (=) sign. Double quotes, as used in the second example, are used when white space is present in the text string you are assigning to the variable. Whenever the shell sees a $variable, such as $ME, it substitutes into the command line the value stored for that variable.

Unfortunately, many of the special characters used by the shell are also used by other programs—there simply are not enough characters to go around. When the special characters shown in Table 8–2 are used in the shell, they must be quoted. Quoting is used when an assigned value contains a special character, spaces, tabs, or new lines. Without the quotes, the special symbols will be interpreted as shell metacharacters instead of being passed as arguments to programs. The three methods of quoting used in the Bourne shell are described in Table 8–1.