**NOTE: This line also might be #!/bin/sh, because bash and sh are just aliases to one another under Linux.**

This line tells the shell what command interpreter to use when running the script. Better yet, it enables you to run shell scripts written for one shell type from within another shell.

After this line, things get more complicated. This section of the chapter is subdivided into smaller sections that focus on different things you might want to do in a script. These sections are ordered in such a way that each section builds on skills you learned in previous sections. Thus, this is one area where it benefits you to read straight through, if you are trying to write a script.

# # Basic Shell Scripting

A shell script consists of commands that can be used directly on the command line. You run a command in a script by typing it just as you would on the command line, though it is wise to be more careful and include the path to the command as well. For example, you could run `ls -la` with just the following line in the script:

```
```
ls -la
```
```

No additional commands or special characters are required. You also may want to set environment or other variables. In the bash shell, you set both shell and environment variables in this format:

```
```
variable=value
```
```

There cannot be any space in between the variable and the equal sign. This helps the shell to know that you are referring to a variable and not a command. You actually use the values of these variables by putting a dollar sign in front of them, such as `$variable`. For example, you might have the following pair of lines in different parts of the script:

```
```
count=10
nextcount=$count + 1
```
```

To assign a string, instead, you would use the following:

```
```
string="This is my string"
```
```

You can also set a variable to be the result of a command by placing the command in backward quotes:

```
```
variable=`command`
```
```