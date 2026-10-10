```
$ echo $OS< Tab>  
$ cd ~ro< Tab>  
$ fing<Tab>  
$ cat /etc/redhat-r< Tab>  
$ mail root@loc< Tab>
```

The first example causes $OS to expand to the $OSTYPE variable. In the next example, ~ro expands to the root user’s home directory (~root/). Next, fing expands to the finger command. After that, /etc/redhat-r expands to /etc/redhat-release, which contains information on your current release of CentOS. Finally, the address of root@loc expands to the computer name localhost.

Of course, there will be times when there are several possible completions for the string of characters you have entered. In that case, you can check the possible ways text can be expanded by pressing [Tab] twice at the point where you want to do completion. The following code shows the result you would get if you checked for possible completions on $P:

```
$ echo $P< Tab>< Tab>  
$PATH        $PPID        $PS1         $PS4
$PIPESTATUS  $PROMPT_COMMAND  $PS2      $PWD
$ echo $P
```

In this case, there are eight possible variables that begin with $P. After possibilities are displayed, the original command line returns, ready for you to complete it as you choose.

If text you are trying to complete is not preceded by a $, ~, or @ (unlike the preceding example), you can still try to complete the text with a variable, username, or hostname. Press the following to complete your text:

+   - [Alt]+ — Complete the text before this point as a username.
+   - [Alt]+$ — Complete the text before this point as a variable.
+   - [Alt]+@ — Complete the text before this point as a hostname.
+   - [Ctrl]+x+~ — List possible username text completions.
+   - [Ctrl]+x+$ — List possible environment variable completions.
+   - [Ctrl]+x+@ — List possible hostname completions.
+   - [Ctrl]+x+! — List possible command name completions.

> **TIP** You may find that only the [Alt] key on the left side of your keyboard works with the preceding examples. Also, remember that characters such as the tilde (~) and dollar sign ($) require the [Shift] key, as well as the [Alt] or [Ctrl] keys.