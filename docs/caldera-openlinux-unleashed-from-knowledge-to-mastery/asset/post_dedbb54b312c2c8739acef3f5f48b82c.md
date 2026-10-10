
## bash Configuration Files

As with most shells, *bash* looks at a number of configuration files upon startup to set initial values and environment variables. Which files get looked at (sourced) and in which order depends on how the shell was started and to some extent on the distribution running it. (OpenLinux, for example, has a somewhat more complex sequence of startup files than *bash* would normally use.)

The normal sequence for a *login* shell (one started from a login prompt or a *bash* started with the *-login* option) is as follows:

- `/etc/profile`
  - bash and Bourne-type shells source this file first. It contains systemwide default values for all Bourne shells.
- `~/.bash_profile`
  - bash then tries to source this bash and user-specific file.
- `~/.bash_login`
  - bash then tries to source this bash and user-specific file.
- `~/.profile`
  - Finally *bash* tries to source this Bourne-type and user-specific file.
- `~/.bash_logout`
  - On exit, it tries to source this file (which 99% of the time only contains the `clear` command to clear the screen).

In OpenLinux, this process is a bit more complicated. The files `~/.bash_profile` and `~/.bash_login` don't exist (in the distribution install). When you log in to OpenLinux, things go like this:

`/etc/profile`

*bash* initially sources this.

`~/.profile`

*bash* then sources this. It is intended to hold user-specific settings for any Bourne-type shell. This then pulls in the next file:

`~/.bashrc`

This is normally used to hold bash and user-specific settings. The OpenLinux distribution, however, intends for this file to hold per-user variables set by the installation. (`.bashrc-private` serves the same purpose in OpenLinux that `.bashrc` normally would.) This then pulls in the next file:

`/etc/config.d/shells/bashrc`

This is the systemwide initialization file for interactive shells (this file is unique to OpenLinux and so is only the case for OpenLinux), which sources:

`~/.bashrc-private`

This file is also unique to OpenLinux and is intended to hold settings for a particular user that would be held in `~/.bashrc` on other systems. After this one is done, control is returned to:

`~/.profile`

which pulls in ...

`/etc/config.d/shells/profile`

This holds systemwide defaults for any Bourne-type login shells (this file, too, is unique to OpenLinux):

`~/.profile-private`

Finally this file is sourced. It is intended to hold user-specific settings for any Bourne-type shell. This again is a pure OpenLinux-ism. In fact, the file doesn’t actually exist in the default OpenLinux install (but if it did it would get sourced).

`~/.bash_logout`

On exit, this file is sourced (which in OpenLinux only contains the command to clear the screen).

Also, interactive shells can source a `~/.inputrc` file, if available (not by default in OpenLinux), to get key bindings.

For an interactive but not login shell (bash without the -login option) only the file `~/.bashrc` is sourced (by bash itself). Of course, in OpenLinux `~/.bashrc` pulls in `/etc/config.d/shells/bashrc` and `~/.bashrc-private`.

Noninteractive shells (generally shells started for or from a program) will source the file pointed to by the BASH_ENV variable and then the ENV variable, if either of those exists.

Also, if bash is invoked as sh (that is, if it is started up as /bin/sh and not /bin/bash) it only sources /etc/profile and ~/.profile (but you have already seen what all those files bring in under OpenLinux).

Basically, configuring bash in OpenLinux boils down to looking at all the preceding files to see what they do. This exercise provides an excellent education in how shell variables and commands work.

You should, however, only need to make changes to ~/.bashrc-private to get the shell configured the way you want it.

## tcsh

tcsh is a modified version of the C shell (csh). It is fully backward-compatible with csh but contains many new features that make user interaction much easier. The biggest improvements over the csh are in the areas of command-line editing and history navigation. You will find that tcsh and bash have much in common, with each shell offering a few “special features” responsible for its uniqueness. A bit of experimentation and familiarity with your own working style will help you determine which of these shells is more comfortable and useful for you.

### Comparing tcsh and bash

The C shell was originally developed by Bill Joy (of Sun fame) while working on BSD UNIX. Basically it was written to approximate C-language syntax in a shell (hence the name) because many programmers found Bourne syntax unpleasant. As it turned out, early versions of csh had some flaws that would pop up most spectacularly and frequently in programming; so, ironically, the shell grew more popular among everyday users as a login shell, while many professionals continued writing programs in sh.

Many of the useful features in bash are present in tcsh and even work the same way (for example, command completion, wildcards, and input/output redirection). Other features, like command history, are similar without being identical; tcsh also offers features not available in bash, such as spelling correction.

### tcsh Command Summary

A brief list of some of the most useful tcsh commands follows:

- **alias** Used to set and display aliases, command nicknames that can be set by the user.
- **bg** Background command. Used to force a suspended process to continue running in the background.
- **bindkey** Allows users to change the editing actions that are associated with a key sequence.
- **cd** Allows users to change the current working directory to the directory specified.
- **exit** Allows the users to terminate the shell.
- **fg** Foreground command. Used to force a suspended process to continue running in the foreground.
- **history** Allows users to display and modify the contents of the history list and the history file.
- **kill** Allows users to terminate another process.
- **logout** Allows users to terminate a login shell.
- **set** Used to set the value of tcsh variables.
- **source** Used to read and execute the contents of a file.
- **unalias** Used to remove aliases that have been defined using the alias command.

Further details and sample usage of these commands may be found in the tcsh man page. At the prompt, type:

```
man tcsh
```

## Command History

The tcsh shell provides a mechanism for accessing the command history that is similar to that in bash. The shell remembers the last $HISTSIZE commands that have been entered into the shell (where $HISTSIZE is a user-definable tcsh variable).

tcsh stores the text of the last $HISTSIZE commands in a history list. When you log in to your account, the history list is initialized from a history file. The default filename for this history file is .history, but you can change it using the $HISTFILE tcsh variable. This file is located in your home directory. (Notice that the file begins with a period. This means that the file is a hidden file and will appear in a directory listing only if you use the -a or -A options of the ls command.)

### Note

In order for the history list to be saved in the history file, you must make sure that the savelist variable is set to the number of commands that you want to be saved.

The simplest way to use the history list is to use the up- and down-arrow keys to scroll through the commands that were entered earlier. Pressing the up-arrow key will cause the last command entered to appear on the command line. Pressing the up-arrow key again will put the command before that on the command line, and so on. If you move up in the command buffer past the command that you wanted, you can move down the history list one command at a time by pressing the down-arrow key.

The command that is on the command line can be edited. You can use the left- and right-arrow keys to move along the command line, and you can insert text at any point. You
