
functions. Note that you must insert a space before and after each curly brace, and you must end the command list with a semicolon.

## SHELL FUNCTION SYNTAX

| Command Form | Meaning |
|---|---|
| `[ function ] name { command1; command2; ... ;}` | Create a function called *name* that includes the specified commands. |
| `name () { command1; command2; ... ;}` | Create a function called *name* that includes the specified commands. |

## EXAMPLES

| This Command | Does the Following |
|---|---|
| `list () { ls -Sh \| less; }` | Creates a shell function called *list* that executes the `ls` command and pipes its output to `less`. |
| `detar () { gunzip *.doc.tar.gz ; tar -xvf *.doc.tar }` | Creates a shell function that unzips all the `*.doc.tar.gz` files and extracts the files from the decompressed `*.doc.tar` archives. |

## Job Control

Normally, processes execute in the *foreground*, which means that they take over the current shell session while running. If you begin an especially time-consuming process, such as compiling a lengthy program, you may wish to place a job in the *background*. By doing this, you regain control of the shell session, and the process executes invisibly. To place a job in the background, you use the **bg** command. You must also give the job a *job ID*, using the syntax discussed in the following table.

## SPECIFYING JOB IDS

| Use This Job ID | To Refer to This Job |
|---|---|
| %n | Job n |
| %string | The job that uses a command with a name starting with *string* |
| %?string | The job that uses a command with a name containing *string* |
| %% | The current job |
| %+ | The previous job |
| %- | The previous job |

## EXAMPLES

| This Command | Does the Following |
|---|---|
| make & | Begins compiling a program and places the process in the background. |
| stop %% | Suspends the current process. |
| Ctrl + z | Suspends the current process. |

## Signals

Linux processes can send *signals* to each other, and each signal has both an identifying number and a fixed message. For example, to kill a process, you use the *kill* command, which sends the *SIGKILL* signal (identified by number 9) to the process. The following table lists the available signals, their ID numbers, and a brief description of the message that each signal sends.

## AVAILABLE SIGNALS

| Signal | Number | Message |
| :--- | :--- | :--- |
| EXIT | 0 | Exit from shell. |
| SIGHUP | 1 | Keep executing even after logout. |
| SIGINT | 2 | Interrupt processing (same as Ctrl + z). |
| SIGQUIT | 3 | Quit. |
| SIGILL | 4 | Illegal instruction. |
| SIGTRAP | 5 | Trace trap. |
| SIGIOT | 6 | Abort. |
| SIGBUS | 7 | Unused. |
| SIGFPE | 8 | Floating-point exception. |
| SIGKILL | 9 | Kill process. |
| SIGUSR1 | 10 | User-defined message. |
| SIGSEGV | 11 | Invalid memory. |
| SIGUSR2 | 12 | User-defined message. |
| SIGPIPE | 13 | Write to a pipe. |
| SIGALRM | 14 | Alarm timeout. |
| SIGTERM | 15 | Terminate. |
| SIGJUNK | 16 | Coprocessor stack fault. |
| SIGCHLD | 17 | Terminate child process. |
| SIGCONT | 18 | Continue processing. |
| SIGSTOP | 19 | Stop. |
| SIGTSTP | 20 | Stop typed at terminal. |
| SIGTTIN | 21 | Background process has tty input. |
| SIGTTOU | 22 | Background process has tty output. |
| SIGURG | 23 | Input/output error. |
| SIGXCPU | 24 | CPU time limit exceeded. |
| SIGXFSZ | 25 | File size limit exceeded. |
| SIGVTALRM | 26 | Virtual alarm clock. |
| SIGPROF | 27 | Profile. |
| SIGWINCH | 28 | Window resize. |
| SIGIO | 29 | Input/output event occurs. |
| SIGPWR | 30 | Power is failing. |

## Alphabetical Command Reference

This section covers the bash commands and Linux utilities relevant to issuing commands, controlling processes, and managing the history list. Note that the commands listed here are *built-in commands*, unless the entry specifically indicates that the command is an ordinary utility (that is, one that is executed from a file). Built-in utilities are made available in memory by the shell.

In this section, you will find commands for doing the following:

- Working more conveniently with commands (**alias**, **chroot**, **fc**, **function**, **hash**, **history**, **script**, **source**, **tee**, **unalias**).
- Managing processes (**bg**, **jobs**, **kill**, **killall**, **nice**, **nohup**, **ps**, **renice**, **suspend**, **times**, **top**, **trap**, **type**).
- Customizing your environment (**bash**, **bind**, **csh**, **export**, **set**, **ulimit**).
- Creating and working with variables (**declare**, **echo**, **env**, **printenv**, **readonly**, **set**).

### alias

*alias name=command*

Creates an alternative name for a command. To create an alias, type the name of your choice followed by an equals sign (=) and the name of an executable command or program, plus options or arguments if you wish (use quotes so that bash processes the options and arguments correctly). If you type alias without an argument, you see a list of all the aliases you have defined, if there are any.

*See also unaliases.*

**EXAMPLES**

| This Command | Does the Following |
|---|---|
| `alias bigfiles='ls -Shl'` | Lists files sorted by size, showing the largest files first. |
| `alias newfiles='ls -tl'` | Lists files sorted by the time of the last modification, showing most recently modified files first. |
| `alias oldfiles='ls -Rtlr'` | Using reverse chronological order (oldest files first), lists all the files in the current directory and all associated subdirectories. |

### bash

`bash [ option ] [ filename ]`

Starts the bash shell. If you specify a filename, bash reads commands from the specified file.

**OPTIONS**

| Use This Option | To Do This |
|---|---|
| `-c string` | Read commands from the specified string. |
| `-i` | Start bash as an interactive shell |
| `-login` | Start bash by reading all the startup files that are consulted when bash is started after you log in |
| `-nobraceexpansion` | Disable brace expansion |
| `-nolineediting` | Disable line editing |
| `-noprofile` | Do not execute the login startup files |
| `--norc` | Do not execute the non-login startup file |
| `-P` | Do not execute any of the current user's startup files |
| `--posix` | Enable POSIX compatibility |
| `--rc *filename*` | Execute the specified filename instead of `~/ .bashrc`. |
| `-S` | Read commands from the standard input (default) |
| `--version` | Show the version number and exit |

### bg

```
bg [ *job ID* ]
```

Places the process specified by *job ID* in the background, as if you had launched the process by appending an ampersand (&).

### bind

```
bind [ *option* ]
```

Displays or adjusts the default key bindings used for bash, which uses the readline program to specify key bindings. To determine the key bindings, bash reads a configuration file named `/etc/inputrc` when it starts. When you log in to your user account, it reads `~/ .inputrc` (a file in your home directory called `.inputrc`). You can change the default key bindings by adding entries to `/etc/inputrc` (so that the changes are available to all users) or to `~/ .inputrc` (so that the changes are available only to the user to whom the directory belongs). You must specify the key bindings using the keymap codes, and you must link the keymap codes to one of the readline functions. For a list of these functions, see the Default Key Bindings table in this section. Examples of keymap codes are \c (Ctrl), \M (Meta), and \v (Escape). To see the keymap code for any key on your keyboard, press Ctrl + v and type the key for which you want to view the code. You can also use bind to assign keys to functions and macros. See the examples in this section for the correct syntax to use when adding entries to these files.

> **TIP** On Intel-based systems, most Linux distributions are configured to map Esc key bindings (signified by the \e code) to the Meta key, which in turn is mapped to the Alt key. To determine the keymap code for any of the keys on your keyboard, use Ctrl + q, Ctrl + v, and press the key.

**OPTIONS**

| Use This Option | To Do This |
| :--------- | :--------- |
| -m keymap | Change the default keymap for the remainder of the session. Alternatives include the following: emacs, emacs-standard, emacs-meta, emacs-ctlx, vi, vi-move, vi-command, and vi-insert. |
| -I | Display the names of all the readline functions. |
| -v | Display current key bindings. |
| -f filename | Read key bindings from the specified filename. |
| -q function | Show the keys, if any, that are bound to the specified function. |

**DEFAULT KEY BINDINGS**

| Readline Function | Default Key Binding |
| :----------- | :----------- |
| abort | ^C-g |
| | ^C-^X^C-g |
| | \e^C-g |
| accept-line | ^C-j |
| | ^C-m |
| backward-char | ^C-b |
| | ^H^OD |
| | \e[D |
