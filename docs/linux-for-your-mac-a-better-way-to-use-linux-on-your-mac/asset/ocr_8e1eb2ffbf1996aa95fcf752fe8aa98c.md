You can then get help on a particular built-in command by again using the help operator and the name of the command:

```
$ help time
time: time [-p] PIPELINE

Execute PIPELINE and print a summary of the real time, user CPU time, and system CPU time spent executing PIPELINE when it terminates.

The return status is the return status of PIPELINE. The ‘-p’ option prints the timing summary in a slightly different format. This uses the value of the TIMEFORMAT variable as the output format.

times: times

Print the accumulated user and system times for processes run from the shell.
```

Another *bash* feature is expansion, particularly command completion. For example, if you type the first few letters of a command's name, then press the Tab key twice, *bash* will provide a list of commands matching the letters like this:

```
$ xp
xp-mapedit xpcd xpirot xplot xpot
xp-replay xpfx xpilots xpix xprompt
xpaint xpet xpinguin xpmtree xprop
xpanex xphoon xpipeman xpshow xpuzzle
xpat2 xpicted xplg xpmtoppm xpyraminx
```

Nearly every *shell* uses important configuration files, also known as *resource* files, and *bash* is no exception. In each user's home directory, you will find at least two (and perhaps three) files:

```
$ ls -af
.bash_history .bashrc /
```

The *.bash_history* file is a *text* file containing a list of previously used command lines. This file is used to display previous commands at the shell prompt ($) when you press the Up or Down arrow keys. The *.bashrc* file contains settings you can customize for your console sessions:

```
$ cat .bashrc
…
#export EDITOR=/usr/bin/pico
#export NNTPSERVER=news.suse.de
…
```