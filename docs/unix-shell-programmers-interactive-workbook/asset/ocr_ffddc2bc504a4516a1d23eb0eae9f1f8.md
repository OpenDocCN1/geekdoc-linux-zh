# Chapter 11: I/O and TRAP Processing 501

j) What is it in the code that makes the variable inWords an array?
Answer: It's the -A option on the second read command.

This option is a very useful feature for this type of application. The variable you name is automatically made into an indexed array with the number of elements equal to the number of tokens obtained by splitting the input line.

> Don't confuse the -A option of the read command with the -A option of the typeset command. With read you get an indexed array, but with typeset you get an associative array.

k) What is the purpose of the statement typeset IFS?

Answer: It guarantees executing this function will not change the value of IFS from whatever value it had beforehand.

Imagine an unwitting user who has set IFS to a colon (:) in order to split the fields, in for example, the PATH variable, then runs mywc. The user would not automatically expect that running your function would affect his or her working environment. A change to IFS could be confusing. The typeset command makes IFS a local variable (Exercise 6.1.4, “Control the Scope of Variables”), so changing it the function will have no effect on the user's environment.

If you wrote mywc as a script instead of as a function you wouldn't need to worry about saving and restoring the value of IFS. The shell gives IFS its default value at the beginning of every script it runs. Functions, however, normally share this variable (and all other variables) with the environment from which they run.

# 11.1.2 ANSWERS

a) What variable is affected by the set typeset command?
Answer: Just the variable x.