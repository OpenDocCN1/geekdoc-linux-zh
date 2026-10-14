
## 7.4.3.2 Using Braces { }

Using braces is valid only in the Bourne, Korn, and POSIX shells.

When commands are grouped in braces, the shell executes them without creating a subshell. In the following example, the shell runs the date command, writing its output to the today.grp file, and then runs the who command, writing its output to today.grp:

```
$ { date; who; } > today.grp
$
```

If the commands were not grouped together with braces, the shell would write the output of the date command to the display and the output of the who command to the file.

The shell recognizes braces in pipelines and command lists, but only if the left brace is the first character on a command line.

## 7.4.4 Quoting

Reserved characters are characters such as the left-angle bracket (<), the right-angle bracket (>), the pipe (|), the ampersand (&), the asterisk (*), and the question mark (?) that have a special meaning to the shell. See Chapter 8 for lists of reserved characters for each operating system shell.

To use a reserved character literally (that is, without its special meaning), quote it with one of the three shell quoting conventions, as shown in Table 7-4.

**Table 7-4: Shell Quoting Conventions**

| Quoting Convention | Action |
|---|---|
| \ | Backslash – Quotes a single character. |
| ' ' | Single quotes – Quotes a string of characters (except the single quotation marks themselves). |
| " " | Double quotes – Quotes a string of characters (except $, `, and \). |

The following sections describe the quoting conventions of Table 7-4 in greater detail.

### 7.4.4.1 Using the Backslash (\ )

To quote a single character, place a backslash (\ ) immediately before that character, as in the following:

```
$ echo \?
?
$
```

This command displays a single question mark (?) character.

### 7.4.4.2 Using Single Quotes (' ')

When you enclose a string of characters in single quotes, the shell takes every character in the string (except the ' itself) literally. Single quotes are useful when you do not want the shell to interpret:

- Reserved characters such as the dollar sign ($), the grave accent (`), and the backslash (\ )
- Variable names

The following example shows how single quotes are used when you want to display a variable name without having it being interpreted by the shell:

```
$ echo 'The value of $USER is' $USER
The value of $USER is amy
$
```

The echo command displays the variable name $USER when it appears within single quotes, but interprets the value of $USER when it appears outside the single quotes.

For information on variable assignments, see Section 7.7.1.

### 7.4.4.3 Using Double Quotes (" ")

Double quotes (" ") provide a special form of quoting. Within double quotes, the reserved characters dollar sign ($), grave accent (`), and backslash (\ ) keep their special meanings. The shell takes literally all other characters within the double quotes. Double quotes are most frequently used in variable assignments.

The following example shows how double quotes are used when you want to display brackets (usually reserved characters) in a message containing the value of the shell variable:

```
echo "<<Current shell is $SHELL>>"
<<Current shell is /usr/bin/csh>>
$
```

For information on variable assignments, see Section 7.7.1.

## 7.5 The Shell Environment

Whenever you log in, your default shell defines and maintains a unique working environment for you. Your environment defines such characteristics as your user identity, where you are working on the system, and what commands you are running.

Your working environment is defined by both environment variables and shell variables. Your default login shell uses environment variables and passes them to all processes and subshells that you create. Shell variables are valid only for your current shell and are not passed to subshells.

The following sections discuss the shell environment, how it is configured, and how you can tailor it.

### 7.5.1 The login Program

Whenever you log in, the login program is run. This program actually begins your login session using data stored in the /etc/passwd file, which contains one line of information about each system user. The /etc/passwd file contains your user name, your password (in encrypted form), your home directory, and your default shell. For more information on the /etc/passwd file, see Chapter 5.

The login program runs after you enter your user name at the login: prompt. It performs the following functions:

- Displays the Password: prompt (if you have a password).
- Verifies the user name and password you entered against what is contained in the /etc/passwd file.
- Assigns default values to the shell environment.
- Starts running the shell process.
- Runs system login scripts and your personal login scripts. See Section 7.6 for more information.

### 7.5.2 Environment Variables

Your shell environment defines and maintains a unique working environment for you. Most of the characteristics of your working environment are defined by environment variables.

Environment variables consist of a name and a value. For example, the environment variable for your login directory is named HOME, and its value is defined automatically when you log in.

Some environment variables are set by the login program, and some can be defined in the login script that is appropriate for your shell. For example, if you use the C shell, environment variables typically will be set in the .cshrc login script. For more information on login scripts, see Section 7.6.

Table 7-5 lists selected environment variables that can be used by all operating system shells. Most of the values of these variables are set during the login process, and are then passed to each process that you create during your session.
