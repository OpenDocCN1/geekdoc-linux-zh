+   3. Save the file, and then use the `chmod` command to change the execute permissions:

```
chmod u+x test2.sh
```

+   4. Run the file:

```
$ ./test2.sh
User info for userid: rich
UID: 1000
HOME: /home/rich
$
```

The `$USER`, `$UID`, and `$HOME` environment variables are commonly used to display information about the logged-in user. The values you see are related to your user account. This allows you to dynamically retrieve information about the user account running your shell script to customize the output.

# User variables

User variables allow you to store your own data within your shell scripts. You assign values to user variables using the equal sign. Spaces must not appear between the variable name, the equal sign, and the value. Here are a few examples:

```
var1=10
var2=23,45
var3=testing
var4="Still more testing"
```

The shell script stores all values as text, but the individual commands interpret the text as numbers or string data. Variables that you define within the shell script are called *local variables*, and are only accessible from within the shell script. Global variables are defined outside of the shell script at the main shell level, and are inherited by the script shell environment.

![](bbox=[0.16, 0.71, 0.24, 0.79])

The `set` command displays all the global variables set. If you need to see the local variables set for your session, use the `printenv` command.

Just like with environment variables, you can reference user variables using the dollar sign. Here's an example of writing a shell script that uses user variables:

```
$ cat test3.sh
#!/bin/bash
# testing variables
```