There are many other environment variables defined by default in Kali Linux. We can view these by running `env` at the command line:

```
``` bash
kali@kali:~$ env
SHELL=/bin/bash
...
PWD=/home/kali
XDG_SESSION_DESKTOP=lightdm-xsession
LOGNAME=kali
XDG_SESSION_TYPE=x11
XAUTHORITY=/home/kali/.Xauthority
XDG_GREETER_DATA_DIR=/var/lib/lightdm/data/kali
HOME=/home/kali
...
TERM=xterm-256color
USER=kali
...
```
```

Listing 32 - Using `env` to show all of the environment variables

# ### 3.1.2 Tab Completion

The Bash shell auto-complete function allows us to complete filenames and directory paths with the [Tab] key. This feature accelerates shell usage so much that it is sorely missed in other shells. Let’s take a look at how this works from the kali user home directory. We’ll start by typing the following command:

```
``` bash
kali@kali:~$ ls D[TAB]
Desktop/  Documents/  Downloads/

kali@kali:~$ ls De[TAB]sktop/

kali@kali:~$ ls Desktop/
```
```

Listing 33 - Illustrating tab completion in Bash

When we hit the [Tab] key the first time after “D”, the Bash shell suggests that there are three directories starting with that letter then presents our partially completed command for us to continue. Since we decide to specify “Desktop”, we then proceed to type “e” followed by the [Tab] key a second time. At this point the Bash shell magically auto-completes the rest of the word “Desktop” as this is the only choice that starts with “De”. Additional information about Tab Completion can be found on the Debian website.<sup>51, 52</sup>

# ### 3.1.3 Bash History Tricks

While working on a penetration test, it’s important to keep a record of commands that have been entered into the shell. Fortunately, Bash maintains a history of commands that have been entered, which can be displayed with the `history` command.<sup>53</sup>

+   51 (Debian-Administration, 2005), https://debian-administration.org/article/316/An_introduction_to_tab_completion,_part_1
+   52 (Debian-Administration, 2005), https://debian-administration.org/article/317/An_introduction_to_tab_completion,_part_2
+   53 (die.net, 2002), https://linux.die.net/man/3/history