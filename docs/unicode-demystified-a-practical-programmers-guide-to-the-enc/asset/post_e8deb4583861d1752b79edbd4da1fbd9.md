
# Builtins (Continued)

| table 14-11 |
| :--- | :--- |
| repeat tcsh | Takes two arguments—a count and simple command lists of commands)—and repeats the command (no pipes or the number of times specified by the count). |
| sched tcsh | Allows you to execute commands at scheduled times. For example, the following command causes the shell to print the message Dental appointment. at 10 AM:
```tcsh
$ sched 10:00 echo "Dental appointment."
```
If you call sched without any arguments, it prints the list of scheduled commands. When the time to execute a scheduled command arrives, tcsh executes the command just before it displays a prompt. |
| set tcsh | Declares, initializes, and displays the values of local variables. Refer to "Variables" on page 698. |
| setenv tcsh | Declares and initializes environment variables. Refer to "Variables" on page 698. |
| shift tcsh | Analogous to the shift builtin (page 583). Without an argument shift promotes the indexes of the argv array. You can use it with an argument to perform the same operation on another array. |
| source tcsh | Executes the shell script given as its argument source does not fork another process. It is similar to the (dot) builtin (page 581). The source builtin expects a TC Shell script, so no leading pound sign is required in the script. The current shell executes so that the script can contain commands, as set, that affect the shell. After you make changes to your .tcshrc or .login file, you can use source to put the changes into effect without logging off and back again. You can nest source builtins. |
| stop tcsh | Stops a job or process that is running in the background. The stop builtin accepts multiple arguments. |
| suspend tcsh | Stops the current shell and puts it in the background. It is similar to the suspend key, which stops jobs running in the foreground. |
| time tcsh | Executes the command that you give it as an argument. It displays a summary of time-related information about the executed command, according to the time shell variable (page 710). Without an argument time displays the times for the current shell and all its children. |
| unmask tcsh | Identifies or changes the access permissions that are assigned to files you create. Refer to page 1366 in Part III for more information on unmask. |
| unalias tcsh | Removes an alias. Refer to "Alias" on page 689. |
| unhash tcsh | Turns off the hash mechanism. See also hashat (page 726) and rehash (page 727). |
| unlimited tcsh | Removes limits on the current process. Refer to the entry "limit" in the table on page 726. |
| unset tcsh | Removes a variable declaration. Refer to "Variables" on page 698. |
| unenv tcsh | Removes an environment variable declaration. Refer to "Variables" on page 698. |
| wait tcsh | Causes the shell to wait for all child processes to terminate. When you give a wait command in response to a TC Shell prompt, it does not display a prompt and does not accept a command until all background processes have finished execution. If you interrupt with the interrupt key, wait displays a list of outstanding processes before returning control of the shell to you. |
| where tcsh | Given the name of a command as an argument, the where builtin locates all occurrences of the command and, for each, tells you whether it is an alias, a builtin, or an executable program in your path. |
| which tcsh | Similar to where but reports only on the command that would be executed, not all occurrences. This builtin is much faster than the GNU/Linux which utility and knows about aliases and builtins. |

# Chapter Summary

The Bourne Again and Z Shells, the TC Shell is both a command interpreter and a programming language. Developed at the University of California at Berkeley, the TC Shell has popular features, such as history, alias, and job control, that have been adopted by other shells.

You may prefer to use tcsh as a command interpreter, especially if you are used to the TC Shell. In case if your default login shell is bash or zsh, you can ask the system administrator to change your login shell to tcsh. The administrator will make the change in the /etc/passwd file, so the shell you requested remains in effect across login sessions, however does not cause tcsh to run your shell scripts; they will continue to run by bash unless you explicitly specify another shell on the first line of the script or invoke one on the command line. Specifying the shell on the first line of your shell scripts ensures the behavior you expect.

If you are used to bash, you will notice some differences between the two shells right away. For instance, the syntax you use to assign a value to a variable differs, and the SPACES around the equal sign are optional. Both numeric and nonnumeric variables are created and given values using the set builtin. The @ builtin can evaluate numeric features for assignment to tcsh using numeric variables.

Because there is no export builtin in tcsh, you must use the setenv builtin to create an environment variable. You can also assign a value to the variable with the setenv command. The command unset removes both local and environment variables, whereas the command unsetenv removes only environment variables.

The syntax of the tcsh alias builtin is slightly different from alias in bash. Unlike bash the tcsh alias feature permits you to substitute command line arguments, using the syntax available with the history mechanism.

Most tcsh features, such as history, word completion, and command line editing, closely resemble their bash and zsh counterparts. The syntax of the tcsh control structures is slightly different but provide functionality equivalent to that found in bash and zsh.

The term globbing, a carryover from the Bourne Again Shell, refers to the matching of names containing special characters (such as * and ?) to filenames. If tcsh is unable to generate a list of filenames matching a globbing pattern, it displays an error message. This is in contrast to bash, which simply leaves the pattern alone.

Standard input and output can be redirected in tcsh, but there is not straightforward to redirect them independently. To do so requires the creation of a subshell that redirects standard output to a file while standard error is available to the parent process.

# Exercises

- 1. Assume that you are working with the following history list:
  37 pine alex
  38 cd /home/jenny/correspondence/business/cheese_co
  39 less letter.0321
  40 vi letter.0321
  41 cp letter.0321 letter.0325
  42 grep hansen letter.0325
  43 vi letter.0325
  44 lp letter*
  45 cd ..//milk_co
  46 pwd
  47 vi wilson.0321 wilson.0329

- 2. How can you identify all the aliases currently in effect? Write an alias named homedos that lists the names (only) of all invisible files in your home directory.

- 3. How can you prevent a command from sending output to the terminal when you start it in the background? What can you do if you start a command in the foreground and later decide that it should run in the background?

- 4. What statement can you put in your .bashrc file to prevent yourself from accidentally overwriting a file when you redirect output? How can you override this feature?

- 5. Assume that the working directory contains the following files:
  adams.ltr.03
  adams.brief
  adams.ltr.07
  abelson.09
  abelson.brief
  anthony.073
  anthony.brief
  azevedo.99

  What happens if you press TAB after typing the following commands?

  - a. less adams.l
  - b. cat a
  - c. Is Ant

  What happens if you press CONTROL-D after typing these commands?

  - e. Is ab
  - f. less a

- 6. Write an alias named backup that takes a filename as an argument and creates a copy of that file with the same name and a filename extension of .bak.

- 7. Write an alias named qmake (quiet make) that runs make with both standard output and standard error redirected to the file make.log. The command qmake should accept the same options and arguments as make.

- 8. How can you make tsh always display the pathname of the working directory as part of its prompt?

# Advanced Exercises

- 9. What lines do you need to change in the Bourne Again Shell script command_menu (page 654) to make it a TC Shell script? Make the changes and verify that it works.

- 10. Users find rm (and even rm -i) too unforgiving because it removes files irrevocably. Create an alias named delete that moves files specified by its argument(s) to the ~/.trash directory. Create a second alias, named undelete, that moves a file from the ~/.trash directory into the working directory. Finally, put the following line in your .logout file to remove any files deleted during the login session:

```
/bin/rm -f $HOME/.trash/* > /dev/null
```

Explain what could be different if the following line were put in your .logout file instead:

```
rm $HOME/.trash/*
```
