$ PATH=/usr/local/bin:$PATH:~/bin

# MAIL: WHERE YOUR MAIL IS KEPT

The **MAIL** variable contains the pathname of the file that holds your mail (your *mailbox*, usually */var/mail/name*, where *name* is your username). If **MAIL** is set and **MAILPATH** (next) is not set, the shell informs you when mail arrives in the file specified by **MAIL**. In a graphical environment you can unset **MAIL** so the shell does not display mail reminders in a terminal emulator window (assuming you are using a graphical mail program).

The **MAILPATH** variable contains a list of filenames separated by colons. If this variable is set, the shell informs you when any one of the files is modified (for example, when mail arrives). You can follow any of the filenames in the list with a question mark (?), followed by a message. The message replaces the **you have mail** message when you receive mail while you are logged in.

The **MAILCHECK** variable specifies how often, in seconds, the shell checks for new mail. The default is 60 seconds. If you set this variable to zero, the shell checks before each prompt.

# PS1: USER PROMPT (PRIMARY)

The default Bourne Again Shell prompt is a dollar sign ($). When you run **bash** with **root** privileges, **bash** typically displays a hashmark (#) prompt. The **PS1** variable holds the prompt string that the shell uses to let you know that it is waiting for a command. When you change the value of **PS1**, you change the appearance of your prompt.

You can customize the prompt displayed by **PS1**. For example, the assignment

$ PS1="[\u@\h \W \]$ "

displays the following prompt:

[user@*host* *directory* *event*]$

where *user* is the username, *host* is the hostname up to the first period, *directory* is the basename of the working directory, and *event* is the event number (page 331) of the current command.

If you are working on more than one system, it can be helpful to incorporate the system name into your prompt. For example, you might change the prompt to the name of the system you are using, followed by a colon and a SPACE (a SPACE at the end of the prompt makes the commands you enter after the prompt easier to read). This command uses command substitution (page 362) in the string assigned to **PS1**:

```
$ PS1="$ (hostname): "
  bravo.example.com: **echo** test
  test
  bravo.example.com:
```