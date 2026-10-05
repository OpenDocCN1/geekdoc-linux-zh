
# PART VI
PROGRAMMING TOOLS

## CHAPTER 27
PROGRAMMING THE BOURNE AGAIN SHELL 953

## CHAPTER 28
THE PERL SCRIPTING LANGUAGE 1041

# 27

## PROGRAMMING THE BOURNE AGAIN SHELL

## IN THIS CHAPTER

- Control Structures ................................. 954
- File Descriptors ................................... 987
- Parameters and Variables ...................... 990
- Array Variables ..................................... 990
- Locality of Variables ............................ 992
- Special Parameters ................................ 994
- Positional Parameters .......................... 996
- Builtin Commands ................................ 1002
- Expressions ........................................ 1016
- Shell Programs .................................... 1024
- A Recursive Shell Script ................. 1025
- The quiz Shell Script ............................ 1028

Chapter 7 introduced the shells and Chapter 9 went into detail about the Bourne Again Shell. This chapter introduces additional Bourne Again Shell commands, builtins, and concepts that carry shell programming to a point where it can be useful. Although you may make use of shell programming as a system administrator, you do not have to read this chapter to perform back to it if and when you like. Feel free to skip this chapter and system administration tasks.

The first part of this chapter covers programming shell structures, also control flow constructs. These structures allow you to write scripts that loop over command-line arguments, make decisions based on the value of a variable, set up menus, and more. The Bourne Again Shell uses the constructs found in such high-level programming languages as C.

The next part of this chapter discusses parameters and variables, going into detail about array variables, local versus global variables, special parameters, and positional parameters. The exploration of builtin commands covers type, which displays information about a command, and read, which allows a shell

953

# CHAPTER 27 PROGRAMMING THE BOURNE AGAIN SHELL

script to accept user input. The section on the exec builtin demonstrates how to use exec to execute a command efficiently by replacing a process and explains how to use exec to redirect input and output from within a script.

The next section covers the tap builtin, which provides a way to detect and respond to operating system signals (as the signal generated when you press CONTROL-C). The discussion of builtins concludes with a discussion of kill, which can abort a process, and getopt, which makes it easy to parse options for a shell script. Table 27-6 lists some of the most commonly used builtins.

The next chapter explores arithmetic and logical expressions as well as the operators that work with them. The final section walks through the design and implementation of two major shell scripts.

This chapter contains many examples of shell programs. Although they illustrate concepts, use more information from earlier examples as well. This overlap reinforces your overall knowledge of shell programming but also demonstrates how you can combine commands to solve complex tasks. Running, modifying, and experimenting with the examples in this book is a good way to become comfortable with the underlying concepts.

# Do not name a shell script test

You can unwittingly create a problem if you give a shell script the name test because a Linux utility has the same name. Depending on how the PATH variable is set up and how you call the program, you may ruin your script or the utility, leading to confusing results.

This chapter illustrates concepts with simple examples, which are followed by more complex ones in sections marked "Optional." The more complex scripts illustrate traditional shell programming practices and introduce some Linux utilities used in scripts. You can skip these sections without loss of continuity. Return to them when you feel comfortable with the basic concepts.

# CONTROL STRUCTURES

The control flow alters the order of execution of commands within a shell script. Control structures include the if...then, for...in, while, until, and case statements. In addition, the break and continue statements work in conjunction with the control structures to alter the order of execution of commands within a script.

# if...then

The if...then control structure has the following syntax:

```
test-command
  then
    commands
```

```
fi
```

![](img/45ff4cd21497435daa35084a84b95d07_1005_0.png)

# **Figure 27-1** An if...then flowchart

The **bold** words in the syntax description are the items you supply to cause the structure to have the desired effect. The **nonbold** words are the keywords the shell uses to identify the control structure.
test builtin Figure 27-1 shows that if the statement tests the status returned by the *test-command* and transfers control based on this status. The end of the if structure is marked by a fi statement (*if* spelled backward). The following script prompts for two words, read them, and then uses an *if* structure to execute commands based on the result returned by the test builtin when it compares the words. (See the test info page for information on the test utility, which is similar to the test builtin.) The test builtin returns a status of *true* if the two words are the same and *false* if they are not. Double quotation marks around *Sword1* and *Sword2* make sure test works properly if you enter a string that contains a *SPACE* or other special character.

```
$ cat if1
echo -n "word 1: "
read word1
echo -n "word 2: "
read word2

if test "$word1" = "$word2"
then
	echo "Match"
fi
echo "End of program."
```

# 956 CHAPTER 27 PROGRAMMING THE BOURNE AGAIN SHELL

```
$ ./if1
word 1: peach
word 2: peach
Match
End of program.
```

In the preceding example the test-command is test "$word1 = "$word2". The builtin returns a true status if its first and third arguments have the relationship specified by its second argument. If this command returns a true status (status = 0), the shell executes the commands between the then and fi statements. If the command returns a false status (not = 0), the shell passes control to the statement following without executing the statements between then and fi. The effect of if this statement is to display Match if the two words are same. The script always displays End of program.

In the Bourne Again Shell, test is builtin—part of the shell. It is also a stand-alone utility kept in /usr/bin/test. This chapter discusses and demonstrates many Bourne Shell builtins. You typically use the builtin version if it is available and the next from it. Each version of a command may vary slightly from one shell to the next and test the utility to any of the shell builtins. See page 1002 for more information on builtins.

The next program uses if structure at the beginning of a script to confirm that you have supplied at least one argument. The test -eq operator compares two integers; the $ special parameter (page 997) takes the value of the number of command-line arguments. This structure displays a message and exits the script with an exit status of 1 if you do not supply at least one argument:

```
$ cat chkargs
if test $ -eq 0
then
  echo "You must supply at least one argument."
  exit 1
```

```
echo "Program running."
$ ./chkargs
You must supply at least one argument.
$ ./chkargs abc
Program running.
```

A test like the one shown in chkargs is a key component of any script that requires. To prevent the user from receiving meaningless or confusing information from the script, the script needs to check whether the user has supplied the appropriate arguments. Some scripts test whether arguments exists (as in chkargs). Other scripts test for a specific number or specific kinds of arguments.

You can use test to verify the status of a file argument or the relationship between two files argument. After verifying that at least one argument has been given on the command line, the following script tests whether the argument is the name of an
