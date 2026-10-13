
Now, any time you enter the `ls` command, it will be as if you typed `ls --color=auto`. Some people, to be safe, alias `rm='rm -i'` to prevent them from accidentally deleting something that they don’t mean to delete. Unfortunately, if they ever log on to a system without this alias, they almost always unintentionally delete something. Therefore, an alias can be a double-edged sword. Of course, if you don’t want this crutch, you can always remove it with `unalias`. An alias always takes precedence over an executable unless the executable is called via its full path (that is, `/bin/ls`). Aliases are not exported, but this is not a problem because they are usually only useful in a shell. Normally, aliases are declared in your `.bashrc` file and are available for each subshell spawned.

**LISTING 14.5 SAMPLE OUTPUT FROM alias**

```bash
alias h='history'
alias j='jobs -l'
alias l='ls -Faf'
alias ll='ls -Alg'
alias ls='ls --color=auto -aF'
alias pd='pushd'
alias which='type -path'
alias z='suspend'
```

Whereas an alias is generally a short command substitution, a function can be a single command or an entire multiline program. Listing 14.6 shows an example of a file called `.functions`. This file is called from the `.bashrc-private` file by the following line:

```bash
. ./.functions
```

As you can see, its syntax is similar to that of a shell script (discussed in a later section), and has the following form:

```bash
name () {statements; }
```

Any functions can be seen from the current shell by using `typeset` or `declare`. This shows your entire environment, including functions. To see functions only, use the `-f` option with either command. See Listing 14.7 for a sample output (notice that the output shows the alias expanded). Functions exist in the current shell, and are an exception to the rule that commands are executed with `fork()` and `exec()`.

**LISTING 14.6 EXAMPLE OF .functions**

```bash
# This is a file with a function

cdd ()
{
    if [ $# = 1 ]; then
        cd $1;
        ls -aF;
    else
        echo "function requires an argument";
    fi
}
```

Functions always execute in the current shell. Functions can supposedly be exported by using `declare -x name`, but I’ve had poor results with this method. As with aliases, though, if the `.functions` file is loaded from the `.bashrc-private` file (as in Listing 14.6), the functions will be available each time a new shell is spawned.

**LISTING 14.7 SAMPLE OUTPUT FROM declare OR typeset**

```bash
declare -f cdd ()
{
    if [ $# = 1 ]; then
        cd $1;
        ls --color=auto -aF -aF;
    else
        echo "function requires an argument";
    fi
}
```

One thing you might have noticed is the way that the `.functions` file is called. The command is preceded by a solitary period (.). This is a synonym for source (which can be substituted for ., but rarely is) and tells the shell to run the command or file in the current shell—that is, to source the file. This causes `exec()` to run without a `fork()`, in a manner similar to functions.

## Customizing Your Environment

By using what you’ve learned previously, you can see that it is a fairly simple task to customize your environment. From within your own home directory, just change or add those things that you want, export them if necessary, and you’re off. Additions and changes can be made from a command line as well as from `.bashrc-private`. Just type the command at a command prompt as you list it in the rc file. This is a great way to experiment.

Take a look at your environment by typing set (or declare if you’re also using functions). If you look down the list, you’ll see something interesting: a UID. This is how the system knows who you are, and what your permissions are. Great! If you change this, you can become root. Sound too easy? A few environment variables have been set with the -r option—they’re read-only. You can’t set them, and you can’t unset them. They’re permanent when declared, and the system has also exported them. Your system administrator can also set environment variables as read-only in files in `/etc`. In certain circumstances, this might be necessary.

If you decide to set a variable from scratch, such as PATH, and it is very long, breaking it up into several lines might be desirable. But how do you do that, when pressing the Enter key executes the line? If the last character in the line is a backslash (`\`), the shell does not execute the line, but waits for more input until you enter a line not terminated by a backslash. You also might notice that your command prompt has changed. This is a signal to you that the shell is awaiting further input. You can see the continuation prompt as the environment variable PS2. PS1 is your primary command prompt, and it can also be customized. You can change your prompt as follows:

```bash
export PS1="$USERNAME@$HOSTNAME \$ "
```

This gives you the prompt `me@myhost $`. You also can change this to always show your present directory (pwd) by using the following:

```bash
export PS1='`pwd` '
```

This brings up the next point. You have four sets of punctuation with which to work. Until this last example, I deliberately stayed with examples that needed only double quotes (" "); but there are also single quotes (' ') and grave quotes (` `). The grave quotes are the quote marks normally found on a 102-key keyboard in the upper-left corner below the Esc key, and to the left of the 1/! key. A shifted grave quote gives you a tilde (~). So when do you use which? The rules are as follows:

- **Use double quotes to pass what’s inside the quotes to the command, but allow variable substitution**—That is, `echo "$HOME"` gives you `/home/username`. You need to use double quotes whenever you have a single argument that contains white space (as defined by your IFS environment variable, usually Space+Tab+Newline). For example, `` cd /etc/modules/`uname -r` `` gives you the error bash did: `cd: /etc/modules/2.0.35/#1: No such file or directory`. Note that the entire name of the directory is `#1 Thu Jul 23 12:41:51 PDT 1998`, but `cd` stopped reading when it reached the first space—between the 1 and the T. So, for this to work properly, you need to surround the argument to `cd` with quotes: `` "/etc/modules/`uname -r`" ``.

- **Use single quotes to pass what’s inside the quotes to the command, but do not allow variable substitution**—That is, `echo '$HOME'` gives you `$HOME`. This is handy if you need to pass `$HOME` to the next command through a pipe without it being expanded first. You’ll need to use this technique in your last command prompt example (shown previously).

- **Use grave quotes to pass what’s inside the quotes to the command, after executing (with variable substitution) the command inside the quotes**—That is, `` echo `pwd` `` gives you `/home/username`.

> **Note**
>
> Currently accepted practice is to use `$(command)` instead of `` `command` ``. This is often easier for new users to grasp, but most scripts written by experienced users still use the grave quotes. Do not confuse `$(command)` with `${variable}`; they’re not interchangeable.

So, the command line required in the previous paragraph, `` export PS1='`pwd` ' ``, is a single quote, then pwd surrounded by grave quotes, a space (for aesthetics), and the closing single quote. By doing this, when you read the environment variable PS1, you’ll see `pwd`. Each time you get a command prompt, it executes pwd and displays it. If you use double quotes instead of single quotes around the argument, you see something such as PS1=/home/username, and the variable does not update each time you change directories. Experiment with it.

You’re probably asking, “But what if I need to use a quote inside a quote?” No problem. I said you had four sets of punctuation, and this is the fourth. But to tell the shell that the quote you’re about to use is not part of the open/close quote sequence, you escape it by preceding it with a backslash (`\`). In fact, the backslash can be used to escape any character the shell can interpret, such as `$`, `*`, and so on. So, `echo \$HOME` produces $HOME.

## Shell Programming (Scripts)

When you’re comfortable with the command-line interface, you’ll find yourself performing some tasks repeatedly. Personally, if I have to do something more than twice, I’ll write a quick script to handle it for me. When you learn how to do this, you have a really powerful ally at your side.

However, writing scripts also necessarily entails a few more steps. For one thing, because you’ll save them (probably in a scripts directory), you’ll want to be able to reuse them. You might also find that you’ll want to have cron run them at night, or when the system is idle, or just daily so that you don’t have to remember to do it yourself. But when you get to this level of sophistication, you’ll need to ensure that your scripts are written to compensate for certain conditions, including the shell to use and the proper environment.

The previous discussions and examples all revolved around one shell, bash, but you know that other shells exist: csh, pdksh, and so on. Scripts written and tested on one shell might very well not work on another. Additionally, when cron runs a script for you, it really doesn’t know about your specific login environment. So, again, the script might fail—but it doesn’t need to.

### Solving the Script Command Dilemma

Solve the first problem, that of the correct shell, at first. On Linux, all files have a “magic number” as determined by the contents of the first two bytes of the file. The file program reads these two bytes and determines what type of file you have. If you expect file to return the fact that the file is a shell script and executable, two things must happen. The first (in Chapter 11, see “File Permissions” section) is to ensure that when it is saved, the execute bit is set, such as `chmod a+x scriptname`. The second is to begin every script the same way:

```bash
#!/bin/bash
```

Using the combination `#!` (sometimes called a *shebang*) as the first two characters in a file ensures that the file is seen by the system as a shell script. The rest of the line is the full path to the program needed to execute the statements in the script. This can be `/bin/perl`, `/usr/bin/awk`, `/usr/bin/sed -f`, and so on. Now, whether run from a C shell or from cron, the system always uses the correct program to execute the code.

### Addressing the Script Environment Quandary

The second problem you need to overcome is the shell environment. We’ve discussed the environment as it applies to a logged-in user, and any script or program run by a logged-in user inherits all exported environment variables in the parent shell. But if cron runs the script, how will the environment look? If you start with the assumption that any environment that cron or any other user might have either doesn’t exist or is wrong, your scripts
