| Special Character | Text Output |
|:---:|:---:|
| \W | The basename of the current working directory (for example, 'cups' instead of '/etc/cups' and 'whil' instead of '~') |
| \V | The history number of this command |
| \# | The command number of this command |
| \$ | If the effective UID is 0, a #; otherwise a $ |
| \\ | A backslash |
| \[ | Begin a sequence of nonprinting characters, which could be used to embed a terminal control sequence into the prompt |
| \] | End a sequence of nonprinting characters |

Here are several examples to get you started. Note that you can just type the command in a command prompt; you don’t have to modify your .bashrc file and save it each time.

| This command | Produces these results |
|:---:|:---:|
| PS1='[\w' | [~] |
| | (when you’re in your home directory) |
| | [/etc/cups/interfaces] |
| | (when you’re in the /etc/cups/interfaces directory) |
| PS1='[\w Dude?' | [~ Dude?] |
| | (when you’re in your home directory) |
| PS1='[\u@\h \w Dude?' | [whil@ffreedom cups] Dude? |
| | (when you’re in the /etc/cups directory) |
| PS1='[\t] [\u@\h:\w]\$' | [21:52:01] [whil@ffreedom:~]$ |

# 5. Change to root inside the command window

You can change to root after opening a command window in one of two ways. The first is by using the "su" command:

```
[whil@ffreedom whil]$ su
Password:
[root@ffreedom whil]#
```

Note that you’re still in the /home/whil directory, but now you’re root. (Referring back to the first item, you’ll note that the title bar has also changed, which means you have “godlike” powers. You can make any change you want to the system, install software, delete files, get into anyone else’s home directory, and so on. This also means, as I’ve said before, that you can do tons of damage. For example, “rm -rf /” will destroy every file on your computer in about five blimpseconds.

The second way you can change to root is by using the “su -” command:

```
[whil@ffreedom whil]$ su -
Password:
[root@ffreedom root] #
```