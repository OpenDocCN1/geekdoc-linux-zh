# Chapter 5: Parameters 213

# PASSING PARAMETERS

Once the shell has broken a command line into tokens and divided it into individual commands, it ends up with a sequence of tokens for each command, beginning with the command name and followed by a sequence of parameters. The parameters, by convention, begin with another optional sequence of option parameters, followed by another optional sequence of positional parameters, as you saw in Chapter 2, "Command Syntax.\ In this lab, the command name is the name of a function or script that you are writing, and you will learn to find out what parameter values were typed on the command line. Dealing with the options will be covered in Lab 5.2, "Processing Option Parameters." For now, you will work with commands and functions that do not use any options.

![](bbox=[0.021, 0.383, 0.116, 0.443])

Options are passed to a script or function the same way that parameters are, so the term positional parameter is used to refer to the parameters after the options. In this lab, there are no options, so the terms parameter-ter positional parameter will always refer to the same thing. In general, an option is a parameter associated with an option letter, and a position parameter is a nonoption parameter that is identified by its ordinal position on the command line (first, second, third, and so forth).

When a shell runs, the command line parameters are assigned to a set of variables named 1, 2, 3... in left-to-right order, that you can reference from within the function or script. In this lab, you will practice looking at the values of those variables using print commands. Once you do that, you will know how to use them for whatever purposes your programs require.

# LAB 5.1 EXERCISES

# 5.1.1 VERIFY YOUR SET-UP

You need directories that the shell will look in for your scripts and definitions. In Chapter 1, "Setting Up," you should have created directories name bin and fun under your home directory for this purpose, if they were not already there. You can use directories with other names if you want to, but all