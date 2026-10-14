To remove a variable itself, regardless of the value it contains, use unset and give the name of the variable.

+   ⇒ To remove a variable called NAME, type:
+   $ unset NAME (RET)

# 3.5.5 Listing Variables

Use set with no options to display all of the variables in your current shell and the values they contain.

+   ⇒ To list all of the variables in your current shell, type:
+   $ set (RET)

# 3.5.6 Changing the Shell Prompt

The special variable PS1 is used for the text of the shell prompt. To change the text of the shell prompt, change the contents of this variable.

+   ⇒ To change your shell prompt to "Your wish is my command: ", type:

```
$ PS1="Your wish is my command: " (RET)
Your wish is my command:
```

Since the replacement text has spaces in it, I’ve quoted it (see Recipe 3.1.3 [Quoting Reserved Characters], page 56).

You can put special characters in the prompt variable in order to output special text. For example, the characters "\w" in the value of PS1 will list the current working directory at that place in the shell prompt text.

+   ⇒ To change your prompt to the default Bash prompt—the current working directory followed by a "$" character—type:

```
$ PS1='\w $ ' (RET)
- $
$
```

The following table lists some special characters and their text output at the shell prompt.