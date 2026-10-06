
# Chapter 12 The Shell II: The Bourne Again Shell

```
$ wc -l letter.txt | cut -cl-7
351
```

Refer to Part III for more information on cut (page 1132) and wc (page 1372).
Another way to get the same result without using cut is to redirect the input to wc instead of having wc get its input from a file on the command line. When you redirect the input, wc does not display the name of the file.

```
$ wc -l < letter.txt
351
```

It is common to assign the result of arithmetic expansion to a variable, as in

```
$ numpages=$ $(wc < letter.txt)/66 + 1
```

The let builtin allows you to evaluate arithmetic expressions without using arithmetic expansion, evaluating each argument you give it as an arithmetic expression. Thus the following is equivalent to the preceding expression:

```
$ let numpages="$(wc < letter.txt)/66 + 1"
```

The double quotation marks keep the SPACES (both those you can see and those that result from the command substitution) from separating the expression into separate arguments to let. The value of the last expression determines the exit status of let: If the value of the last expression is 0, the exit status of let is 1; otherwise, the exit status is 0.

You can let multiple arguments on a single command line:

```
$ let a=5+3 b=7-2
$ echo a $b
```

When you refer to variables when doing arithmetic expansion with either let or $(expression), the shell does not require you to bind the variable name with a dollar sign ($), although it is a good practice to do so, as in most places you you must. The following two assignments assign the same value to numpages:

```
$ let numpages=numpages+1
$ let numpages=$numpages+1
```

## Word Splitting

The IFS (Internal Field Separators) shell variable specifies the characters that you can use to separate arguments on a command line and has the default value of SPACE TAB NEWLINE. Regardless of what IFS is set to, you can always use one more SPACE or TAB characters to separate arguments on the command line, provided that these characters are not quoted or escaped. When you assign IFS the value of characters, these characters can also separate fields, but only in the event that they undergo expansion. This type of interpretation of the command line is called word splitting. The following example demonstrates how setting IFS can affect the interpretation of a command line:

```
$ a=w:x:y:z
$ cat $a
cat: w:x:y:z: No file or directory
$ IFS=""
$ cat $a
cat: w: No such file or directory
cat: x: No such file or directory
cat: y: No such file or directory
cat: z: No such file or directory
```

The first time cat is called, the shell expands the variable a, interpreting the string w:x:y:z as a single token to be used as the argument to cat. The cat utility cannot find a file named wxyz. After IFS is set to a colon (:), the shell expands the variable into four words as separate arguments to cat w, x, y, and z. Word splitting based on the colon (:) takes place only after the variable is expanded.

The shell splits expanded words on a command line according to the separating characters found in IFS. When there is no expansion, there is no splitting. Consider the following commands:

```
$ IFS="p"
$ export IFS
```

Although IFS is set to p, nothing was expanded on the export command line, so the word export was not split. The following example uses variable expansion to produce the export command:

```
$ IFS=p
$ aa=export
$ echo $aa
2 files to edit
ort: new file: 
1 more files to edit
:q
```

This time there was expansion, and the character p in the token interpreted as a separator, so the effect of the command line is to start the shell with two filenames:

## Be Careful When Changing IFS

Although sequences of SPACE or TAB characters are treated as single separators, each occurrence of another field acts as a separator. Changing IFS has a variety of side effects so change it cautiously. You may find it useful to first save the value of IFS before changing it; you can easily get unexpected results. Or you can fork a new shell with bash or zsh to get back to your old shell, where IFS is working properly. You can also set IFS to its default value with the following command:

```
$ IFS=$
```

## Pathname Expansion

Pathname expansion (page 157) is the process of interpreting ambiguous file references and substituting them with the appropriate filenames. The shell performs this when it encounters an ambiguous file reference—a token containing any of the characters *, [. If the shell is unable to locate any files that match the specified pattern, the ambiguous file reference is left alone. The shell does not delete the token or replace it with a null string but passes it to the program. In the first echo command the shell expands the three tokens (tmp1, tmp2, and tmp3) to echo, which displays the three filenames passed by the shell. After rm removes the three tmp files, the shell finds no filenames that match tmp* when it tries to expand it.

Variable expansion makes possible for you to assign to a variable value that includes special characters, such as an asterisk (*). In the next example the working directory has three files whose names begin with tmp. When you assign the value tmp* to the variable var, the shell does not expand the ambiguous file reference, because it occurs in the value of a variable (in the assignment statement for the variable). No quotation marks are around the string tmp*. Context alone prevents the expansion. After the assignment, the set builtin (with the help of grep) shows the value of var to be tmp*.

The echo commands demonstrate three levels of expansion. When $var is quoted with single quotation marks, the shell performs no expansion and passes the character $var to echo, which echo displays. When you use double quotation marks, the shell performs variable expansion and substitutes the value of var for its name, preceded by a dollar sign. There is no filename expansion on this command because double quotation marks suppress it. In the final command, the shell, without the limitations of quotation marks, performs variable substitution and pathname expansion before passing the arguments to echo:

```
$ ls tmp
tmp1 tmp2 tmp3
$ var=tmp*
$ set | grep var
var=tmp*
$ echo '$var'
$var
$ echo "$var"
tmp*
$ echo $var
tmp1 tmp2 tmp3
```

## Command Line Expansion

Putting double quotation marks around an argument causes the shell to suppress pathname and all other expansion except parameter and variable expansion. Putting single quotation marks around an argument suppresses all types of expansion. In the following example the variable $alex is between double quotation marks, which allow parameter expansion, so the shell expands the variable to its value. This expansion does not occur when single quotation marks allow pathname expansion; the last two commands display the expanded argument:

```
$ echo tmp* $alex
tmp1 tmp2 tmp3
$ echo "tmp* $alex"
tmp* $alex
$ echo 'tmp* $alex'
```

## Chapter Summary

The shell is both a command interpreter and a programming language. As a command interpreter, the shell executes commands you enter in response to its prompt. When you use it as a programming language, the shell executes commands from files called shell scripts.

You typically run a shell script by giving its name on the command line. To run a script in this manner, you must have execute permission for the file holding the script. Otherwise the shell does not know that the script is executable. Alternatively, you can execute the script by entering bash, tsh, or zsh followed by the name of the file on the command line. Either way you need read permission for the file.

Job control is not part of the Bourne Again Shell but is included in the Job Shell, which is identical to the Bourne Again Shell. A job is one or more commands connected by pipes. You can bring a job running in the foreground with the [fg] builtin into the background with the [bg] builtin, provided that it is first suspended by pressing the suspend key.

Each process has a unique identification, or PID, number when you give it a command, the shell forks a new (child) process to execute the command, unless the command is built into the shell (see page 670 for a partial list of builtins). While the child process is running, you can run a child process in the background and bypass the sleep state with the ampersand (&), so the shell prompt returns immediately after you press RETURN. Each command in a shell process terminates, it returns its exit status to its parent process: Zero signifies success, and nonzero signifies failure.

The shell allows you to define variables. You can declare and initialize a variable by assigning a value to it; you can remove a variable declaration by using unset. Variables are usually local to a process and must be exported by the [export] or [setenv] builtin to make them available to child processes. The shell also defines the positional and special parameters which are defined by dollar signs in the following table to reflect the only manner in which you can reference them. Unlike shell variables, you cannot assign values to them.
