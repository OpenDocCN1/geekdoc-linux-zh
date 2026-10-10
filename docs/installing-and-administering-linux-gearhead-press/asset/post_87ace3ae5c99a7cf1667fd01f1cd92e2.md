
## Listing the Values of Individual Variables: The echo Command

If you want to check to see what a variable is set to, simply enter the `echo` command followed by a dollar sign and the name of the variable, as such:

```
$ echo $variablename<Enter>
```

Note that you add a space between the *echo* command and the dollar sign but not between the dollar sign and the name of the variable being referenced.

### Example 11.2 Using echo $ to Check Variable Settings

Sancho works in the `tcsh` shell. He asks Don Quixote, who he knows works in the `bash` shell, whether the Don's path variable contains `/usr/games`. The Don enters

```
$ echo $PATH<Enter>
/usr/local/bin/:bin:/usr/bin:/usr/X11R6/bin:/home/quixote/bin
```

Both realize that */usr/games* is not specified in either of their PATHS.

## Setting Shell Variables

User-defined variables can hold any type of data (for example, integer numbers, single words, text strings, or complex numbers). It is up to the application referencing the variable to decide what to do with the contents. In contrast, the content of system-defined variables is fairly static and inflexible. For example, the `HOME` variable can contain only a directory and *not* a file.

When we say “set shell variables,” we mean “specify, or set, the *value* of a variable.” The values of variables can be set in two ways:

- By a form of direct definition called *variable substitution*
- To the output of a command or a group of commands, which is called command substitution. Command substitution is discussed later in this chapter.

We will look at each technique in turn.

### Variable Substitution: Setting Variable Values with the Equals Sign

There are two ways to use variable substitution. This first method is simple and straightforward and does not really rely on the “character substitution” aspect of variable substitution, which we will illustrate in the next section.

When setting the values of variables, the commands differ depending on the shell you are using. To set a variable when you are in the *bash* or *pksh* shell, use the equals sign with the name of the variable (existing or new) on the left side and the value you want to set for the variable on the right side:

```
$ variablename=value<Enter>
```

There are *no* spaces between the characters. To set a variable in the *tcsh* shell, on the other hand, use the `set` command:

```
$ set variablename = value<Enter>
```

In the *tcsh* case, spaces appear on both sides of the equals sign. See Example 11.2 for setting variables in all three shells.

**NOTE** The man page for each shell generally describes the syntax used to set their respective prompts. Do not forget—if you are in the *tcsh* shell and you want to export variables and their values to the terminal environment, you have to use `setenv` instead of `export`.

### Example 11.3 Setting Variable Values with the Equals Sign (=)

Both Don Quixote and Sancho find that the commands they type tend to require more than one line. But the secondary prompt (PS2) variable, the simple right angle bracket symbol, tends to confuse them occasionally and they make mistakes on the second line. Here is how they each change their respective secondary prompts. Because he works in the *bash* shell, the Don sets the PS2 variable as follows (similar to the *pksh* shell):

```
$ PS2="Please Continue ">"<Enter>
```

Sancho, who uses the `tcsh` shell, types

```
$ set PS2 = "More ><Enter>"
```

The variable substitution in Example 11.3 is reminiscent of the latter part of Chapter 7, where we used a backslash followed by Enter to interrupt a long command on one line so that we could continue typing the command on the next line. We mentioned that the greater-than sign ($>$) was assigned to the secondary prompt through the value of the `PS2` variable.

Thus, in Example 11.3, the Don and Sancho changed from the secondary prompt $>$ to a text string to avoid confusion with the standard out redirection symbol. Note that to do so, they each had to include double quotation marks at each end of the text string. If they did not use the double quotation marks, they would have received an error message beginning with `bash: syntax error.` So, whenever you set a variable with a text string, always enclose the text string in double quotation marks.

## Variable Substitution Using Character Substitution

This method is a handy technique that can save you keystrokes almost every day. We will define it the best we can here, but to get the best grasp of it, we refer you to Example 11.4. In this case, examples work best.

Begin by defining variables and specifying values for them as you have done before. For the bash shell,

```
$ variablename=value<Enter>
```

Then, as you create correspondences, memos, and such, you insert the variable names right into your text using a dollar sign as the first character of the variable name. Then, when the time comes, the shell will substitute the value of the variable for the variable name you typed.

Look closely at Example 11.4. It illustrates some typical and successful variable definition and substitution scenarios. But one scenario produces unexpected and incorrect results.

> **NOTE** To set a variable equivalent to a string of text, surround the text string with double quotation marks.

### Example 11.4 Setting Variables by Character Substitution

Juana is learning to use the character substitution technique to save her some time when she is organizing Lady Dulcinea’s schedule. She finds that she uses the word *day* in many situations. So, she will try to create a variable called *abc* and assign the value day to it. Here, she sets and verifies the *abc* variable:

```
$ abc=day<Enter>
$ echo $abc<Enter>
day
```

Now, she checks to see whether it works by substitution:

```
$ echo Tomorrow is Tues$abc<Enter>
Tomorrow is Tuesday
```

So far so good. It works when no space appears *before* the variable. The substitution is not hampered.

But here, something seems to go wrong. The shell tries but fails to substitute:

```
$ echo There will be a $abclong meeting<Enter>
There will be a meeting
```

When no space is encountered *after* the variable name, the shell was tricked into looking for the wrong name. In this case, it searched in vain for a variable it thought was called *abclong*, which we know did not exist because we did not define it. When the shell could find no definition for this (wrong) variable name *abclong*, it returned with a null string. That is, the shell did not make a substitution but rather, removed the portion of the statement containing the wrong or undefined variable name.

To try again to substitute, this time successfully:

```
$ echo There will be a ${abc}long meeting<Enter>
There will be a daylong meeting
```

When you cannot have a space following the variable name, you can preserve the proper variable name by surrounding it with curly brackets ( ). Note, however, that $ must remain *outside* the curly brackets. Otherwise, the shell will not be “triggered” to perform the substitution.

## Setting Shell Variables by Command Substitution

In the preceding discussion of variable substitution, you saw how to specifically place a value into a variable. In this section, we discuss how to place the result of command execution into a variable.

In Linux's bash shell, you can accomplish command substitution by using two types of syntaxes:

```
$ variablename=`command (-options) [arguments]`
```

and

```
$ variablename=$(command (-options) [arguments])
```

The first syntax example uses back quotes (not single quotes) to surround the command whose output you want to assign as the value of the variable. The back quote key (‘ ` ’) is located immediately to the left of the 1 key. Do not confuse the back quote with single quotation marks.

Back quotes are supported by the classic Bourne and C shells, so they are supported also by the bash and tcsh shells. Back quotes are supported by the Korn shell for backward compatibility.

The second type of syntax, variablename=$(command … , etc.), was originally specific to the Korn shell.

### Example 11.5 Command Substitution: Variable Values Set to Command Results

Freston, while performing several of his routine administration functions, makes use of command substitution. In the following code, he will define a variable called now and for its value substitute the output of the date command:

```
$ date<Enter>
Mon Jul 16 16:14:34 CST 2001
```

He sets the variable to contain the results of the command:

```
$ now=`date`<Enter>
```

or
