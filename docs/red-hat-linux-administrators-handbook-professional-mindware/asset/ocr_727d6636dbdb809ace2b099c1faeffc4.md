The ispell program allows you to correct spelling mistakes in a text file in an interactive fashion. If you have a misspelling in the file, the program suggests a spelling and gives you options to replace it with a correctly spelled word. This is the spell checker for text files.

# msg

Syntax: **msg [ y | n ]**

The msg program allows you to enable or disable public write access to your terminal. For example,

```
msg y
```

enables write access to your terminal such that another user on the same system can use the write command to write text messages to you. The n option allows you to disable write access. If you do not want to be bothered by anyone at any time, add msg n to your login script (.login) file.

# write

Syntax: **write *username* *tty***

The write program allows you to write text messages to the named user if she has not disabled write access to her TTY. For example, the following command enables you to type a text message onscreen:

```
write shoeman
```

When you finish the message by pressing Ctrl+D, the message is displayed on user shoeman's terminal. If the user is logged in more than once, you have to specify the terminal name, as well. For example,

```
write shoeman tty00
```