# ### Globbing

*Globbing* is a function that expands file names (wildcards) using a pattern-matching behavior. The wildcards that globbing interprets are the * symbol, the ? symbol, sets of characters that are included within brackets, and special characters such as the ^ symbol.

# ## Tab Completion

*Tab completion* facilitates auto completion of commands and file names. Pressing the **Tab** key completes the names of commands, files, directories, users, and hosts.

![](bbox=[0.76, 0.19, 0.82, 0.25])

```
<pre><code>[root@localhost ~]# his
hisaxctrl history
[root@localhost ~]# his</code></pre>
```

*Figure 9-3:* Tab completion entries for the text "his".

![](bbox=[0.02, 0.59, 0.09, 0.64])

Pressing the **Tab** key twice displays all files and directories that begin with the string you typed.

# ## The history Command

The *history command* is used to view previously typed commands. It retrieves the specified number of commands from the ~/.bash_history file. You can use the **Up Arrow** or **Down Arrow** key to select the desired command. By simultaneously pressing **Alt** and **Plus Sign ( + )** , you can recall arguments that have been used with previously executed commands.

![](bbox=[0.76, 0.72, 0.82, 0.78])