
## How a Function Works

Declaring a function can be done on the command line, the syntax of which is as follows:

```
function funcname () { cmd -opts args }
```

A function can also be defined as a multiline entity by using a script file to hold common functions, rather than declaring them on the command line. For example, to declare the script *funk*, you can put the following into a script file and then use the source or . commands to make the function active:

```
funk() {
    ps;
    ls --color=tty -ld;
    who
}
```

## Viewing, Setting, and Removing Functions

To see the functions defined for your user, use the `declare` command:

```
declare -F
```

This returns output similar to the following:

```
declare -f funk

declare -f fish

declare -f iliad
```

The `declare` command can also be used to see the contents of a particular function, such as

```
declare -f funk
```

This returns output similar to this:

```
funk() {
    ps;
    ls --color=tty -ld;
    who
}
```

To see everything that can be easily pulled about a particular function, use the `type` command:

```
type -all funk
```

This returns output similar to the following:

```
funky is a function
funky ()
{
  ps;
  ls -color=tty -ld;
  who
}
```

To set a function in memory, you use the format discussed previously. The following example does three simple and separate tasks that must be delimited by a semicolon (;) character, particularly including the last one after the who command.

This command declares the function funky:

```
funky () { ps ; ls -ld ; who ; }
```

Executing this function is simple; you just enter it on the command line:

```
funky
```

This returns output similar to what's shown here:

| PID | TTY | TIME | CMD |
|:----|:----|:-----|:----|
| 4960 | pts/3 | 00:00:00 | bash |
| 5609 | pts/3 | 00:00:00 | ps |

drwxr-x--- 17 root root 8192 Apr 14 15:01 .
root tty1 Apr 8 17:26
root pts/1 Apr 14 14:41 (192.168.1.100)
root pts/0 Apr 8 17:31 (:0)
root pts/2 Apr 12 14:42 (:0)
root pts/3 Apr 14 14:44 (192.168.1.100)

The components of a function can be anywhere from simple to very complex, with just about anything that a script can contain being valid for a function.

Removing a function is relatively simple: If it has been defined in a file such as the .bashrc, you can unset the function for only the current login session with the following command:

```
unset funky
```

No output is returned—the function just disappears and returns again upon the next login shell.

To remove a function defined on the command line, the same command string is used. A simple logout and login again also refreshes the original session.

Functions are usually defined in the .bashrc file for a given user or in the /etc/bashrc file for all users. The syntax is exactly the same as on the command line, and functions are typically defined after any aliases because aliases are capable of being included in functions.

> **ALERT** Expect some questions about functions on the exam, including what a function is; how to create, modify, and remove them; how to view them; and what the correct syntax of a function is comprised of.

## Understanding Shell Levels

One of the mysteries I want to clear up in this section is what happens to variables that are declared and exported when the shell exits.

For example, take the situation where you have an environment variable named **CHEESE** with a value of *wensleydale* and then you run a script where the same value is exported with a different value. It's important to know what happens to the value of the original, and also to the value of the latest exported version of the variable.

Here's how it works, step by step:

1. Open a shell session.

2. Declare and export the variable **CHEESE** with the following command:

   ```
   export CHEESE=wensleydale
   ```

3. Echo the value of **CHEESE** with the command shown here:

   ```
   echo $CHEESE
   ```

   This returns the following output:

   ```
   wensleydale
   ```

4. With the assurance that your variable contains the right value, create and save the following script in vi or your favorite editor:

   ```bash
   #!/bin/bash
   # filename = scriptfile
   echo $CHEESE is set to $CHEESE
   export CHEESE=gouda
   TYPE=$CHEESE
   echo "$TYPE is very good"
   echo $CHEESE is set to $CHEESE
   ```

5. Now set the file to be executable:

   ```
   chmod +x scriptfile
   ```

6. Run the script with the following command:
   `./scriptfile`
   This produces the following output:
   ```
   CHEESE is set to wensleydale
   The gouda is very good
   CHEESE is set to gouda
   ```

7. Finally, echo the value of $CHEESE again:
   `echo $CHEESE`
   This produces the output shown here:
   `wensleydale`

Let's deconstruct this script, so you can see what happened to the original value and why it's still there, even though you exported a different value for $CHEESE. Let's take the script line by line:

- **Line 1**—The shebang that sets which shell to use
- **Line 2**—A comment reminding you what the filename is
- **Line 3**—The echo of the original value of $CHEESE
- **Line 4**—The tricky export of the new value for $CHEESE
- **Line 5**—The incorporation of $CHEESE as the value for TYPE
- **Line 6**—An echo showing that the new values work
- **Line 7**—An echo of the damning evidence, or so it appears

The key to all this tomfoolery with variable values and exporting of those values is to remember that the use of the export command makes the exported variable and its value available to the current shell and all subshells. In other words, when you run the script, it runs in a subshell of the current shell, which is why the original value for $CHEESE is available to the script. However, when you exit the script (and the subshell), the exported value of $CHEESE declared within the script goes away with the subshell, leaving the original value of $CHEESE.

> **ALERT** This concept is key for the exam. You will be tested on your knowledge of how subshells and variable exports work. Many mistake the export of a variable as being the equivalent to making that variable available throughout the system, when it's really available only for the current shell and subshells.

There is almost always another way to do something in Unix and Linux, so I must finish with how you can execute a script in the current shell. If you remember the concept of sourcing, or using the `source` command to take a script and make its variables active for your current shell, that is the method you can use to run a script file in the current shell, if necessary. For example, you can run the script `scriptfile` in the current shell with either of these two command strings:

```
source scriptfile
. scriptfile
```

Outside of sourcing configuration files so their contents act on the current shell, you'll probably not see or use sourcing to run scripts.

## Exam Prep Questions

1. What would you call the feature of the **bash** shell that allows a string to be typed that would then call another string that contains variables and recursive actions that is contained in memory?

   - A. Script
   - B. Alias
   - C. Function
   - D. Program

Answer **C** is correct because only a function has the necessary capabilities, particularly recursive actions such as looping. Answer **A** is incorrect because a script is not contained in memory; it’s on disk. Answer **B** is incorrect because an alias has most of the features but doesn’t allow recursive actions. Answer **D** is incorrect because a program is binary and exists on disk until executed.

2. Enter in the exact command string used to declare an alias named that executes the following commands:

`ps ; file *`

The correct answer is `alias ='ps ; file *'`. There are no alternative correct answers.

3. On a Linux system installed with the default shell, you need to execute a shell script that contains variables, aliases, and functions by simply entering its name on the command line. What should be the first line of the script? (Choose all that apply.)

   - A. Nothing
   - B. `/#bin/csh`
   - C. `/#bin/sh`
   - D. `exec=/#bin/bash`
   - E. `/#1/bin/bash`

Answers **A**, **C**, and **E** are correct because the features mentioned as being in the script are all related to the **bash** shell. Either you use answer **E** to specifically set it or you allow the default of **bash** to be used by not specifying a shell, and on a default Linux system, `/#bin/sh` is a link to `/#bin/bash`. Answer **B** is incorrect because the syntax is incorrect for the string and the **csh** shell won’t do what the question requires. Answer **D** is incorrect because the line is incorrect and means nothing in a shell script.
