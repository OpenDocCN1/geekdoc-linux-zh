# Tip

Even with arrow-key navigation, you might find yourself having to repeatedly scroll into your history to find a frequently invoked but complicated command. The bash shell has another trick up its sleeve: the ^r command, which searches your history for the most recent match of whatever you type. Press ^r and then type a few letters, and your command line will automatically be filled out with the latest matching command you entered.

The history mechanisms of the shells are wonderful time-savers when you’re working with files. I find myself using the bash !! and !word mechanisms daily either to repeat intricate commands (such as the preceding example, in which I built up a very complex command, step by step) or to repeat the most recently used edit commands. Table 14.1 summarizes the available bash history mechanisms. I encourage you to learn and use them. They will soon become second nature and save you lots of typing as you proceed.

| Command | Function |
|---|---|
| !! | Repeat the last command. |
| !$ | Repeat the last word of the preceding command. |
| !* | Repeat all but the first word of the preceding command. |
| ^a^b | Replace a with b in the preceding command and then re-invoke it. |
| !ptrn | Repeat the most recent command that starts with ptrn. |
| !n | Repeat command number n from the history list. |

# TABLE 14.1 Bash History Commands

# Task 14.3: Command Aliases

If you think the history mechanism has the potential to save you typing, you’ll be glad to learn about the command-alias mechanism in bash and ksh. Using aliases, you can easily define new commands that do whatever you’d like, or you can even redefine existing commands to work differently, have different default flags, or more!

The general format for using the alias mechanism in both shells is alias word=commands. If you enter alias without any specified words, the output shows a list of aliases you have defined. If you enter alias word, the output lists the current alias, if there is one, for the specified word.

+   1. One of the most helpful aliases you can create specifies certain flags to ls so that each time you enter ls, the output will look as though you used the flags with the command. I like to have the -F flag set:

Click here to view code image

```
% ls
Archives      awk script      dickens.note      src
InfoWorld     bin              keylime.pie       temp
```