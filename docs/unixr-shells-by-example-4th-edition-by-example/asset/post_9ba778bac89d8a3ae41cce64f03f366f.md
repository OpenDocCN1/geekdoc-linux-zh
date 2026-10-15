
## EXAMPLE 13.6 (CONTINUED)

```
1  set -o vi
2  set -o noclobber
3  set -o ignoreeof
4  alias rm='rm -i'
   alias cp='cp -i'
   alias mv='mv -i'
5  stty erase ^H
   # Source global definitions
6  if [ -f /etc/bashrc ]; then
       . /etc/bashrc
   fi
7  case "$-" in
       *i*) echo This is an interactive bash shell
           ;;
       *)  echo This shell is noninteractive
           ;;
   esac
10 history control=ignoredups
11 function cd { builtin cd $1; echo $PWD; }
```

## EXPLANATION

- 1. The set command with the -o switch turns on or off special built-in options. (See “The set -o Options” on page 763.) If the switch is -o, a minus sign, the option is turned on, and if a plus sign, the option is turned off. The vi option allows interactive command-line editing. For example, set -o vi turns on interactive command-line editing, whereas set -o vi turns it off. (See Table 13.1 on page 764.)
- 2. The noclobber option is turned on, which prevents the user from overwriting files when using redirection; for example, sort filex > filex. (See “Standard I/O and Redirection” on page 844.)
- 3. When exiting a shell, normally you can type ^D (Ctrl-D). With ignoreeof set, you must type exit.
- 4. The alias for rm, rm -i, causes rm to be interactive (-i), that is, it will ask the user if it’s okay to remove files before actually removing them. The alias for the cp command, cp -i, causes the copy to be interactive.
- 5. The stty command is used to set the terminal backspace key to erase. ^H represents the Backspace key.
- 6. If a file called /etc/bashrc exists, source it.
- 7. If the shell is interactive, the special variable, $-, will contain an i. If not, you are probably running a script. The case command evaluates $-.
- 8. If the value returned from $- matches *i* (i.e., any string containing an i), then the shell prints This is an interactive bash shell.

9 Otherwise, the shell prints This shell is noninteractive. If you start up a script or a new shell at the prompt, you will be able to tell whether your shell is interactive. It is only here to let you test your understanding of the terms “interactive” and “noninteractive” shell.

10 The history_control setting is used to control how commands are saved in the history file. This line reads: Don’t save commands in the history file if they’re already there; that is, ignore duplicates.

11 This is a user-defined function. When the user changes directories, the present working directory, PWD, is printed. The function is named cd and contains within its definition the command cd. The special built-in command, called builtin, precedes the cd command within the function definition to prevent the function from going into an infinite recursion; that is, from calling itself indefinitely.

The /etc/bashrc File. Systemwide functions and aliases can be set in the /etc/bashrc file. The primary prompt is often set here.

## EXAMPLE 13.7

```
(Sample /etc/bashrc)

# Systemwide functions and aliases
# Environment stuff goes in /etc/profile

# For some unknown reason bash refuses to inherit
# PS1 in some circumstances that I can’t figure out.
# Putting PS1 here ensures that it gets loaded every time.

1 PS1="[\u@\h \W]\$ "
2 alias which="type -path"
```

## EXPLANATION

1 Systemwide functions and aliases are set here. The primary bash prompt is set to the name of the user (\u), and @ symbol, the host machine (\h), the basename of the current working directory, and a dollar sign. (See Table 13.2 on page 769.) This prompt will appear for all interactive shells.

2 Aliases, nicknames for commands, are usually set in the user’s .bashrc file. The alias was preset and is available when bash starts up. You use it when you want to find out where a program resides on disk; that is, what directory it is found in (e.g., which ls will print /bin/ls).

## The ~/.profile File.

The .profile file is a user-defined initialization file. It is found in the user's home directory, and sourced once at login if running sh (Bourne shell). Because this file is used by the Bourne shell, it should not contain any bash-specific settings. If running bash, .profile will be run if bash cannot find any other of the initialization files listed previously. It allows a user to customize and modify his or her shell environment. Environment and terminal settings are normally put here, and if a window application or database application is to be initiated, it is started here.

## EXAMPLE 13.8

```
(Sample .profile)
# A login initialization file sourced when running as sh or the #.bash_profile or
# .bash_login are not found.

1 TERM=xterm
2 HOSTNAME=`uname -n`
3 EDITOR=/bin/vi
4 PATH=/bin:/usr/ucb:/usr/bin:/usr/local:/etc:/bin:/usr/bin:.
5 PS1="HOSTNAME $ > "
6 export TERM HOSTNAME EDITOR PATH PS1
7 stty erase ^h
8 go () { cd $1; PS1=`pwd`; PS1=`basename $PS1`; }
9 trap 'HOME/ logout' EXIT
10 clear
```

## EXPLANATION

- 1. The TERM variable is assigned the value of the terminal type, xterm.
- 2. Because the uname -n command is enclosed in backquotes, the shell will perform command substitution; that is, the output of the command (the name of the host machine) will be assigned to the variable HOSTNAME.
- 3. The EDITOR variable is assigned /bin/vi. Programs such as mail and history will now have this variable available when defining an editor.
- 4. The PATH variable is assigned the directory entries that the shell searches in order to find a UNIX/Linux program. If, for example, you type ls, the shell will search the PATH until it finds that program in one of the listed directories. If it never finds the program, the shell will tell you so.
- 5. The primary prompt is assigned the value of HOSTNAME, the machine name, and the $ and > symbols.
- 6. All of the variables listed are exported. They will be known by child processes started from this shell.
- 7. The stty command sets terminal options. The Erase key is set to ^H, so that when you press the Backspace key, the letter typed preceding the cursor is erased.
