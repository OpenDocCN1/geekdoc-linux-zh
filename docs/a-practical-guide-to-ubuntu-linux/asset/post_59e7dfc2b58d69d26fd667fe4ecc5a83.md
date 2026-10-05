K Shell System UNIX introduced the Korn Shell (ksh), written by David Kohn. This shell extended many features of the original Bourne Shell and added many new features. Some features of the Bourne Again Shell, such as command aliases and command-line editing, are based on similar features from the Korn Shell.

POSIX The POSIX (Portable Operating System Interface) family is being developed by PASC (IEEE's Portable Application Standards Committee, www.posix.org). A comprehensive FAQ on POSIX, including many links, appears at www.opengroup.org/austin/papers/posix_faq.html.

POSIX 1003.2 describes shell functionality. The Bourne Shell provides the features that match the requirements of this standard. Efforts are under way to make the Bourne Again Shell fully comply with the POSIX standard. In the meantime, if you invoke bash with the --posix option, the behavior of the Bourne Shell will closely match the POSIX requirements.

## SHELL BASICS

This section covers using startup files, redirecting standard error, writing and executing shell scripts, separating and grouping commands, implementing job control, and manipulating the directory stack.

## chsh: changes your login shell

The person who sets up your account determines which shell you use when you first log in the system or when you open a terminal emulator window in a GUI environment. Under Ubuntu, bash is the default shell. You can run any shell you like once you are logged in. Enter the name of the shell you want to use (bash, tsh, or another shell) and press RETURN; the next prompt will be of the new shell. Give an exit command to return to the previous shell. Because shells you call in this manner are nested (one runs on top of the other), you will be able to log out from your original shell. When you have nested shells, keeping exit commands until you reach your original. You will then be able to log.

Use the chsh utility to change your login shell permanently. First give the command chsh. In response to the prompt, enter your password and the absolute pathname of the shell you want to use (/bin/bash, /bin/tsh, or another shell). When you change your login shell in this manner using a terminal emulator (page 125), subsequent terminal windows will not reflect the change until you log out and log back in. See page 457 for an example of how to use chsh.

## STARTUP FILES

When a shell starts, it runs startup files to initialize it. Which files the shell depends on whether it is a login shell, an interactive shell that is not a login shell, or a noninteractive shell (one used to execute shell scripts). Ubuntu puts appropriate commands in some of these files. This section covers startup files.

## LOGIN SHELLS

The files covered in this section are executed by login shells and shells that start with the --login option. Login shells are, by nature, interactive. The shell first executes the commands in /etc/profile. A user working with root privileges can set up this file to establish systemwide default characteristics for users. The next shell looks for ~/.bash_profile, ~/.bash_login, and ~/.profile (~ is shorthand for your home directory), in order it executes the commands in the file. You can put commands in one of these files to override the defaults in /etc/profile. A shell running on a virtual terminal does not execute commands in these files. When you log out, bash executes commands in ~/.bash_logout. This file often holds commands that clean up after a session.

## INTERACTIVE NONLOGIN SHELLS

The commands in the preceding startup files are not executed by interactive, nonlogin shells. However, although not called by bash directly, many ~/.bashrc files call /etc/bashrc. This setup allows a user working with root privileges to establish systemwide default characteristics for nonlogin shells. An interactive nonlogin shell for a login shell, such as ~/.bash_profile, runs this file, so both login and nonlogin shells run the commands in ~/.bashrc.

## NONINTERACTIVE SHELLS

The commands in the previously described startup files are not executed by noninteractive shells, such as those that run shell scripts. However, these shells inherit login shell variables that are set by startup files.

## BASH_ENV

Noninteractive shells look for the environment variable BASH_ENV (or the shell is called as sh) and execute commands in the file named by this variable.

## SETTING UP STARTUP FILES

Although many startup files and types of shells exist, usually all you need are the .bash_profile and .bashrc files in your home directory. Commands similar to following in .bash_profile run commands for login shells (when .bashrc exists). With this setup, the commands in .bashrc are executed by login nonlogin shells.

```bash
if -f ~/.bashrc ]; then ~/.bashrc; fi
```

The -f ~/.bashrc tests if the file .bashrc in your home directory exists. Sees pages 955 and 957 for more information on test and its synonym. See page 296 for information on the dot builtin.

## Use bash_profile to set PATH

Because commands in .bashrc may be executed many times, and because shells inherit exported variables, it is a good idea to put commands that add variables to the .bash_profile file. For example, the following command adds the bin subdirectory of the home directory to PATH (page 319) and should go in .bash_profile:

```bash
PATH=$PATH:$HOME/bin
```

When you put this in .bash_profile and not in .bashrc, the PATH variable added only once, when you log in. Modifying a variable in .bash_profile causes changes you make in an interactive session to aggregate. In contrast, modifying a variable in .bashrc overrides changes inherited from a parent shell.

Sample .bash_profile and .bashrc files follow. Some commands used in these files are not covered later in this chapter. In any startup file, you must export variables and functions that you want to be available to child processes. For more information refer to "Locality of Variables" on page 992.

```bash
$ cat ~/.bash_profile
if -f ~/.bashrc ]; then # Read local startup file if it exists
fi
PATH=$PATH:\$(pwd) # Add the working directory to PATH
# Set prompt
```

The first command in the preceding .bash_profile file executes the commands in the user's .bashrc file if it exists. The next command adds to the PATH variable (page 319). Typically PATH is set and exports /etc/profile so it does not need to be exported in a user's startup file. The final command sets and exports PS1 (page 321), which controls the prompt.

A sample .bashrc file is shown on the next page. The first command executes the commands in the /etc/bashrc file if it exists. The next file sets and exports the LANG (page 326) and INIT (for vim initialization) variables and defines several aliases. The final command defines a function (page 349) that swaps the names of files.

## (Dot) or source: RUNS A STARTUP FILE IN THE CURRENT SHELL

After you edit a startup file as .bashrc, you do not have to log out and log in to put the changes into effect. Instead, you can run the startup file using the (dot) or source builtin (they are the same command). With all other commands, the . must be followed by a SPACE on the command line. Using or source is similar to running a script file, except these commands run the script as part of the current process. Consequently, when you use, . or source to run a script, changes you make to variables from within the script affect the shell you run it from. If you run a startup file as a regular script and did not use it, the variables created in the startup file would remain in effect only in the subshell running.

```bash
$ cat ~/.bashrc
if [ -f /etc/bashrc ]; then
    source /etc/bashrc
fi
```

## CHAPTER 9 THE BOURNE SHELL

```bash
# function to exchange the names
function switch() {
    # of two files
    local tmp=$1
    mv "$1" $tmp
    mv "$2" "$1"
    mv $tmp "$2"
}

# 296
# 295
# 319
# 321
# 326
# 343
# 344
# 345
# 346
# 349
# 125
# 457
# 955
# 957
# 992

# always interactive
alias df='df -h'
# set up aliases
alias lr='ls -ltrh'
# - interactive
alias rm='rm -i'
# history
alias h='history'
# chmod
alias ch='chmod 755 '
```
