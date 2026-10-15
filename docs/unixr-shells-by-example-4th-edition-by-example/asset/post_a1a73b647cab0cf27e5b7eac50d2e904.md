
## EXAMPLE 8.46 (CONTINUED)

```
1 names=Tom:Dick:Harry:John
2 OLDFS="$IFS"    # Save the original value of IFS
3 IFS=":"
4 for persons in $names
 do
5    echo Hi $persons
done
6 IFS="$OLDFS"    # Reset the IFS to old value
7 set Jill Jane Jolene    # Set positional parameters
8 for girl in $@
 do
9    echo Howdy $girl
done
```

(The Output)

```
5 Hi Tom
 Hi Dick
 Hi Harry
 Hi John
9 Howdy Jill
 Howdy Jane
 Howdy Jolene
```

## EXPLANATION

1 The names variable is assigned the string Tom:Dick:Harry:John. Each of the words is separated by a colon.

2 The value of IFS, whitespace, is assigned to another variable, OLDFS. Because the value of the IFS is whitespace, it must be quoted to preserve it.

3 The IFS is assigned a colon. Now the colon is used to separate words.

4 After variable substitution, the for loop will iterate through each of the names, using the colon as the internal field separator between the words.

5 Each of the names in the wordlist are displayed.

6 The IFS is reassigned its original value stored in OLDFS.

7 The positional parameters are set. $1 is assigned Jill, $2 is assigned Jane, and $3 is assigned Jolene.

8 $@ evaluates to all the positional parameters, Jill, Jane, and Jolene. The for loop assigns each of the names to the girl variable, in turn, through each iteration of the loop.

9 Each of the names in the parameter list is displayed.

## 8.7 Functions

Functions were introduced to the Bourne shell in AT&T's UNIX System VR2. A function is a name for a command or group of commands. Functions are used to modularize your program and make it more efficient. You may even store functions in another file and load them into your script when you are ready to use them.

Here is a review of some of the important rules about using functions.

- 1. The Bourne shell determines whether you are using a built-in command, a function, or an executable program found on the disk. It looks for built-in commands first, then functions, and last, executables.
- 2. A function must be defined before it is used.
- 3. The function runs in the current environment; it shares variables with the script that invoked it, and lets you pass arguments by assigning them as positional parameters. If you use the exit command in a function, you exit the entire script. If, however, either the input or output of the function is redirected or the function is enclosed within backquotes (command substitution), a subshell is created and the function and its variables and present working directory are known only within the subshell. When the function exits, any variables set there will be lost, and if you have changed directories, you will revert to the directory you were in before invoking the function. If you exit the function, you return to where the script left off when the function was invoked.
- 4. The return statement returns the exit status of the last command executed within the function or the value of the argument given, and cannot exceed a value of 255.
- 5. Functions exist only in the shell where they are defined; they cannot be exported to subshells. The dot command can be used to execute functions stored in files.
- 6. To list functions and definitions, use the set command.
- 7. Traps, like variables, are global within functions. They are shared by both the script and the functions invoked in the script. If a trap is defined in a function, it is also shared by the script. This could have unwanted side effects.
- 8. If functions are stored in another file, they can be loaded into the current script with the dot command.

### FORMAT

```
function_name () { commands ; commands; }
```

## EXAMPLE 8.47

```
dir () { echo "Directories: "; ls -l | awk '/^d/ {print $NF}' ; }
```

## EXPLANATION

The name of the function is dir. The empty parentheses are necessary syntax for naming the function but have no other purpose. The commands within the curly braces will be executed when dir is typed. The purpose of the function is to list only the subdirectories below the present working directory. The spaces surrounding the curly braces are required.

### 8.7.1 Unsetting Functions

To remove a function from memory, the unset command is used.

### FORMAT

```
unset function_name
```

### 8.7.2 Function Arguments and the Return Value

Because the function is executed within the current shell, the variables will be known to both the function and the shell. Any changes made to your environment in the function will also be made to the shell. Arguments can be passed to functions by using positional parameters. The positional parameters are private to the function; that is, arguments to the function will not affect any positional parameters used outside the function.

The return command can be used to exit the function and return control to the program at the place where the function was invoked. (Remember, if you use exit anywhere in your script, including within a function, the script terminates.) The return value of a function is really just the value of the exit status of the last command in the script, unless you give a specific argument to the return command. If a value is assigned to the return command, that value is stored in the $? variable and can hold an integer value between 0 and 255. Because the return command is limited to returning only an integer between 0 and 255, you can use command substitution to capture the output of a function. Place the entire function in backquotes and assign the output to a variable just as you would if getting the output of a UNIX command.

## EXAMPLE 8.48

```
(Using the return command)
(The Script)
#!/bin/sh
# Scriptname: do_increment
1 increment () {
2   sum= `expr $1 + 1`
3   return $sum   # Return the value of sum to the script.
}
```
