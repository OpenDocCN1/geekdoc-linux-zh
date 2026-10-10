same results as you did with the longer command from Example 8.2. Try the following:

```
$ find . -name 'm*' -ls<Enter>
```

# ## The find Command with an Interactive Single Action

In the previous example, the second action was not drastic. When it ex-
ecuted, it did not impact the directory structure, contents or the file con-
tents. But what if that second action was a little more drastic? What if, for
example, Sanko had wanted to remove the entries that find found?
What if he had not entered the appropriate options or arguments? What if
he had not entered m* instead of m1*? He might have accidentally deleted
his mbox and memos files.

So, in some cases, we see that interaction between the second process
and the terminal might be useful. This section focuses on how to add such
interactivity to the find command by adding the -ok option. This time,
instead of just going ahead and performing the second command, Linux
prompts the user for verification before proceeding, as shown in Example
8.3. The prompt asks a basic yes or no question; to respond, the user types
y, yes, n, or no and then presses Enter.

The advantage to this interaction option is that the user has the ability to
monitor the action and prevent inadvertent problems that might develop
as a result of execution of the action. The syntax is as follows:

```
$ find directory(es) conditions -ok commandname options { } ;
```

Consider using -ok with find in the following situations:

+   * **When your search pattern might not be or cannot be absolutely
+     accurate** (or absolutely surgical, if you are only trying to affect some
+     entries and not all of them) and you do not want to affect any entries
+     unnecessarily.

+   * **When your second command is fairly final.** In Example 8.3, we are
+     removing the successful find candidates, and that action is pretty
+     final. If we were doing this action noninteractively and something
+     were to go wrong, however, we would have to find a way to restore
+     the entries we did not want to remove. This process could prove
+     costly in some situations.