# # LAB 4.2 EXERCISES

# ## 4.2.1 EVALUATE SIMPLE VARIABLES

The easiest way to see the effects of evaluating a variable is to put a reference to it in a print statement. You have already done this in Chapter I, “Setting Up,” when you checked your PATH and FPATH variables. Because we want to see the effects of assigning new values to variables in this lab, those two variables are not good ones to study; changing them could adversely affect your setup. Instead, this lab will use a variable whose value you see every time you enter a command.

Everyone gets tired of the default prompt string, $, sooner or later, and the shell provides a variable to let you customize it to almost any extent you wish. Each time the shell displays a prompt for you to enter a command, it does so by evaluating and printing the variable named PS1.

# ## SETTING UP FOR THIS LAB

If you have already customized your prompt string, run the following command so your interactions will start looking like the ones in these exercises:

```
PS1="$ "
```

> Don't skip these exercises even though you already know how to customize your prompt string. The exercises deal with principles of using variables, and they use the prompt string only as an example that makes it easy to see the effects of your work.

Now run the following command:

```
print $PS1
```

+   a) Explain the output.