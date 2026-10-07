So what happens if more than one file in the directory begins with the letter *r*? It would seem that this would cause a problem if you wanted to use command-line completion. Let's see what happens when you have the following directory contents:

`News/  bin/  mail/  samplefile  test/  tools/  working/`

Now you have *two* files in the directory that start with the letter *t*. Assuming that you still want to `cd` into the `test` subdirectory, how do you do that using command-line completion? If you type `cd t<tab>` as you did before, *bash* does not know which subdirectory you want to change to because the information you have given is not unique.

*bash* then beeps to notify you that it does not have enough information to complete the command. After beeping, *bash* leaves the command on the screen as it was entered. This enables you to enter more information without retyping what was already typed. In this case, you only need to enter an **e** and press the **Tab** key again. This gives *bash* enough information to complete the command on the command line for you to verify:

```
cd test
```

If instead you decide that you want to `cd` into the `tools` subdirectory, you can type:

```
cd t<tab>
```

This gives *bash* enough information to complete the command.

Whenever you press the **Tab** key while typing a command, *bash* tries to complete the command for you. If it can't complete the command, it fills in as much as it can and then beeps, notifying you that it needs more information. You can then enter more characters and press the **Tab** key again, repeating this process until *bash* displays the desired command.

# # Wildcards

Another way that *bash* makes typing commands easier is by enabling users to use wildcards in their commands. The *bash* shell supports three kinds of wildcards:

+   * `*` matches any character and any number of characters.
* `?` matches any single character.
* `[...]` matches any single character contained within the brackets.

The `*` wildcard can be used in a manner similar to command-line completion. For example, assume the current directory contains the following files:

`News/  bin/  games/  mail/  samplefile  test/`