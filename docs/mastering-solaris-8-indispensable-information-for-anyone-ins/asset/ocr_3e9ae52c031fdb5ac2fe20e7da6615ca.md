A *here document* allows you to script the interaction of a program from within another script. It is called a here document because it is immediately accessible in the shell script. A *function* is a group of commands that are parsed before storage into main memory. Faster than shell scripts, functions may be used over and over. There are several ways to define functions. You may use the command line or place one within a script, or if you want to retain a function for more than one login session, you can define it in your `.profile` file. It can then be called by giving its name along with other arguments.

Solaris utilities are important in the Bourne shell. The `find` utility performs both simple and complex tasks. It is most often used to find files in the system, but it has many other uses. Shortcuts (like using brackets around arguments to call up the `test` built-in, which automatically tests the arguments) make routine tasks easier to remember and carry out. Square brackets are synonymous with the `test` built-in and make a script easier to follow. However, because `test` is rarely used anymore, it is recommended that you use the brackets surrounding the arguments instead.

Standard techniques are part of a shell script. To be well written, a script needs to adhere to techniques that verify, report command errors, and redirect informational messages to standard error.

The Bourne shell, although not the most voluminous of the three shells, has some sophisticated capabilities for getting the job done. A little practice with writing shell scripts and using control structures will fine-tune a program as well as a user's skills. There is a sh-compatible shell in every distribution of Unix, so familiarity with the Bourne shell is the first step in becoming proficient with all of the Unix systems as well as Solaris 8.

# # Control Structures

The execution of commands with a shell script can be altered by the use of what are called *control flow commands*, or *control flow structures*. Based on Boolean logic, these structures consist of statements that test a condition. The following sections discuss the control flow structures that are used most often in the Bourne shell.

# ## The if...then structure

The `if...then` statement is a common example of a control flow structure:

```
If test-case; then

commands

fi
```