+   f) What does tee do?

All of the commands in this pipeline are well-known UNIX filters. If you are not already familiar with them, it would be worth your while to look them up and set up some similar pipelines to practice using the various options they support. You are encouraged to share your favorite pipeline with others at the companion web site for this book, located at: http://www.phptr.com/phptrinteractive/

# 3.1.4 CONDITIONAL COMMANDS
&& AND OR ||

In this exercise, you will learn two operators that are designed specifically for use in scripts, even though you will use the shell's interactive mode to look at them.

EXIT CODES
To understand how these operators work, you need to know that each command you run behind an exit code that you can test to determine whether the command completed "normally" or "not normally." (The command itself decides what its exit code will be; you'll see how to do this for your own functions and scripts in Chapter 7, "Basic Tests") For now, you can think of these exit codes as logic values, where normal completion is indicated by a value of "true" and not-normal completion is indicated by a value of "false."

The shell has a pair of built-in commands named true and false that do nothing but set their exit codes and terminate. In this lab, we will use these two commands to substitute for "real commands" that set their exit codes based on what happens when they run.