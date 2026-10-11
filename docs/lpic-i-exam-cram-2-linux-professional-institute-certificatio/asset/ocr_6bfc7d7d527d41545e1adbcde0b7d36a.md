Another facet of substituting commands is to enclose the command itself between parentheses and declare it as a variable, as in this example:
```
file $(grep -irl crud /usr/src/linux-2.4)
```

The main reason to use a command substitution like this is it allows you to nest commands within commands. Rather than having to use wildcards, you just use the right substitution.

# # bash's History Feature

The history command shows the stack of previously executed commands. bash's history function depends on a variable called HISTFILE, normally set to the current user's .bash_history file (located in the user's home directory). When echoed, it returns the full path and name of the user's history file, like so:
```
echo $HISTFILE
/home/rbrunson/.bash_history
```

When a user logs in with either a login or interactive/non-login shell, the user's .bash_history file is opened. Normally, the history stack is not written to the .bash_history file until the user logs out of that shell session. In the case of a user logging in and then executing a bash subshell to the login shell, the subshell reads the parent shell's history file and writes to it upon exit. You can see this happen if you do the following steps:

+   1. Log in to a machine as a user.
+   2. Execute the following command:
+      ```
+   echo "this is the main shell history"
+      ```
+   3. Then start a new shell:
+      ```
+   bash
+      ```
+   4. In the new shell, execute the following:
+      ```
+   history
+      ```
+   5. Execute these commands:
+      ```
+   echo "this is the subshell history"
+   history
+      ```
+   6. Exit the subshell with the following command:
+      ```
+   exit
+      ```