
## Searching History

At any time, we can view the contents of the history list by:

```
```bash
[me@linuxbox ~]$ history | less
```
```

By default, bash stores the last 500 commands you have entered. We will see how to adjust this value in a later chapter. Let's say we want to find the commands we used to list `/usr/bin`. One way we could do this:

```
```bash
[me@linuxbox ~]$ history | grep /usr/bin
```
```

And let's say that among our results we got a line containing an interesting command like this:

    88  ls -l /usr/bin > ls-output.txt

The number “88” is the line number of the command in the history list. We could use this immediately using another type of expansion called *history expansion*. To use our discovered line we could do this:

```
```bash
[me@linuxbox ~]$ !88
```
```

bash will expand “!88” into the contents of the eighty-eighth line in the history list. There are other forms of history expansion that we will cover a little later.

bash also provides the ability to search the history list incrementally. This means that we can tell bash to search the history list as we enter characters, with each additional character further refining our search. To start incremental search press Ctrl-r followed by the text you are looking for. When you find it, you can either press Enter to execute the command or press Ctrl-j to copy the line from the history list to the current command line. To find the next occurrence of the text (moving “up” the history list), press Ctrl-r again. To quit searching, press either Ctrl-g or Ctrl-c. Here we see it in action:

```
```bash
[me@linuxbox ~]$
```
```

First press Ctrl-r:

## History Expansion

The shell offers a specialized type of expansion for items in the history list by using the "!" character. We have already seen how the exclamation point can be followed by a number to insert an entry from the history list. There are a number of other expansion features:

Table 8-6: History Expansion Commands

| Sequence | Action |
|---|---|
| !! | Repeat the last command. It is probably easier to press up arrow and enter. |
| !number | Repeat history list item number. |
| !string | Repeat last history list item starting with string. |
| !?string | Repeat last history list item containing string. |

I would caution against using the "!string" and "!?string" forms unless you are absolutely sure of the contents of the history list items.

There are many more elements available in the history expansion mechanism, but this subject is already too arcane and our heads may explode if we continue. The HISTORY EXPANSION section of the bash man page goes into all the gory details. Feel free to explore!

> **script**
> 
> In addition to the command history feature in bash, most Linux distributions include a program called script that can be used to record an entire shell session and store it in a file. The basic syntax of the command is:
> 
> `script [file]`
> 
> where file is the name of the file used for storing the recording. If no file is specified, the file typescript is used. See the script man page for a complete list of the program's options and features.

## Summing Up

In this chapter we have covered some of the keyboard tricks that the shell provides to help hardcore typists reduce their workloads. I suspect that as time goes by and you become more involved with the command line, you will refer back to this chapter to pick up

more of these tricks. For now, consider them optional and potentially helpful.

## Further Reading

- The Wikipedia has a good article on computer terminals:
- http://en.wikipedia.org/wiki/Computer_terminal

## 9 – Permissions

Operating systems in the Unix tradition differ from those in the MS-DOS tradition in that they are not only *multitasking* systems, but also *multi-user* systems, as well.

What exactly does this mean? It means that more than one person can be using the computer at the same time. While a typical computer will likely have only one keyboard and monitor, it can still be used by more than one user. For example, if a computer is attached to a network or the Internet, remote users can log in via SSH (secure shell) and operate the computer. In fact, remote users can execute graphical applications and have the graphical output appear on a remote display. The X Window System supports this as part of its basic design.

The multiuser capability of Linux is not a recent "innovation," but rather a feature that is deeply embedded into the design of the operating system. Considering the environment in which Unix was created, this makes perfect sense. Years ago, before computers were "personal," they were large, expensive, and centralized. A typical university computer system, for example, consisted of a large central computer located in one building and terminals which were located throughout the campus, each connected to the large central computer. The computer would support many users at the same time.

In order to make this practical, a method had to be devised to protect the users from each other. After all, the actions of one user could not be allowed to crash the computer, nor could one user interfere with the files belonging to another user.

In this chapter we are going to look at this essential part of system security and introduce the following commands:

- `id` – Display user identity
- `chmod` – Change a file's mode
- `umask` – Set the default file permissions
- `su` – Run a shell as another user
- `sudo` – Execute a command as another user
- `chown` – Change a file's owner
