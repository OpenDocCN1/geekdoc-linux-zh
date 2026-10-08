
# Environment Variables

environ(5) for descriptions of the following environment variables that affect the execution of cronab: LC_TYPE, LC_CTYPE, and NL_PATH.

EDITOR Determine the editor to be invoked when the -e option is specified. The default editor is ed(1). If both the EDITOR and VISUAL environment variables are set, the value of the VISUAL variable is used as the editor.

# Exit Status

- 0 Successful completion.
- >0 An error occurred.

# Files

- /etc/cron.d Main cron directory.
- /etc/cron.d/cron.allow List of allowed users.
- /etc/default/cron Contains cron default settings.
- /etc/cron.d/cron.deny List of denied users.
- /var/cron/log Accounting information.
- /var/spool/cron/crontabs Spool area for crontab.

# Attributes

attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWcs |

# See Also

atq(1), atrm(1), auths(1), ed(1), sh(1), cron(1M), su(1M), auth_attr(4), new attributes(5), environ(5)

# crtplot — Graphics Filters for Various Plotters

## Synopsis
/usr/ucb/plot [-Terminal]

## Description
See plot(1).

# crypt — Encrypt or Decrypt a File

## Synopsis
/usr/bin/crypt [password]

## Description
crypt encrypts and decrypts the contents of a file. crypt reads from the standard input and writes on the standard output. The password is a key that selects a particular transformation. If no password is given, crypt demands a key from the terminal and turns off printing while the key is being typed in. crypt encrypts and decrypts the same key, as shown in the following example.

```
castle@ crypt key < clear.file < encrypted.file
castle@ crypt key < encrypted.file | pr
```

Files encrypted by crypt are compatible with those treated by the editors ed(1), ex(1), and vi(1) in encryption mode.
The security of encrypted files depends on three factors:

- The fundamental method must be hard to solve.
- Direct search of the key space must be infeasible.
- "Sneak attacks" by which keys or cleartext become visible until minimized.

crypt implements a one-rotor machine designed along the lines of the German Enigma, but with a 256-element rotor. Methods of attack on such machines are widely known; thus, crypt provides minimal security.
The transformation of a key into the internal settings of the machine is deliberately expensive to design, that is, to take a substantial fraction of a second to compute. However, if keys are restricted to (say) their lowercase, then encrypted files can be read by spending only substantial fraction of five minutes of machine time.
Because the key is an argument to the crypt command, it is potentially visible to users executing ps(1) or a derivative command. To minimize this possibility, crypt destroys any record of the key immediately on entry. No doubt the choice of keys and key security are the most vulnerable aspect of crypt.

## Files
/dev/tty For typed key.

# csh

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNWsu |

# See Also

ed(1), ex(1), ps(1), vi(1), attributes(5)

# csh - Shell Command Interpreter with a C-like Syntax

## Synopsis
/usr/bin/csh [-bceinstv/xx] [argument...]

## Description
csh, the C shell, is a command interpreter with a syntax reminiscent of the C language. It provides a number of convenient features for interactive use that are not available with the Bourne shell, including file-name completion, command aliasing, history substitution, job control, and a number of built-in commands. As with the Bourne shell, the C shell provides variable, command and file-name substitution.

> Note - Although the shell is robust enough for general use, adventures in its esoteric periphery may reveal unexpected quirks.

## Initialization and Termination

When first started, the C shell normally performs commands from the .cshrc file in your home directory, provided that it is readable and you own it or your real group matches its group ID. If the shell is invoked with a name that starts with a dash (-), as started by login(1), it runs as a login shell.

If the shell is a login shell, it is invoked in the following sequence:

1. Execute commands in /etc/
2. Execute commands from the .cshrc file in your home directory.
3. Execute commands from the .login file in your home directory; the same permission checks as those for .cshrc are applied to this file. Typically, the .login file contains commands to terminate the terminal type and environment.

As a login shell, it performs commands from the .login file in your home directory; the same permission checks as those for .cshrc are applied to this file.

## Interactive Operation

After processing is complete, an interactive C shell begins reading commands from the terminal, prompting with hostname(or hostname# for superuser). The shell then repeatedly performs the following actions:

1. Reads a line of command input and breaks it into words.
2. Puts the sequence of words in the history list and then parses them.
3. Executes commands from-line.

## Noninteractive Operation

When the shell's input is not a terminal, the # introduces a comment that continues to the end of the line. Its special meaning is suppressed when preceded by \ or in matching characters.

## Options

- -b: Batch mode.
- -c: Command string.
- -e: Exit on error.
- -f: Disable globbing.
- -i: Interactive mode.
- -n: Noninteractive mode.
- -s: History file.
- -t: Terminal type.
- -v: Verbose mode.
- -x: Print commands.
- -z: Set history limit.

## Lexical Structure

The shell splits inputs into words at space and Tab characters, except as noted below. The characters &, |, ;, <, > and ) separate words; if paired, the pairs form single words. These characters can be made part of other words by escaping them. A word preceded by \ is equivalent to a space.

In addition, a string enclosed in single quotes (''), double quotes (""), or brackets ([]) forms a partial word; in such a string, including any space or Tab characters, do not separate words. Pairs of quote (\') or double quote (") characters, a newline preceded by a backslash (\) gives a true newline Additional functions of each type of quote are described, under Variable Substitution, Command Substitution, and File-name Substitution.

> Note - Words can be no longer than 1,024 bytes. The system limit argument lists to 1,048,576 bytes. However, the maximum number of arguments to a command for which file-name expansion is 1,706. Command substitutions may extend to no more characters than are allowed in the argument list. To detect looping, the shell restricts the number of alias substitutions on a single line to 20.

# Command-Line Parsing

A simple command is composed of a sequence of words. The first word (that is not part of an IO redirection) specifies the command to execute. A simple command, or a set of commands separated by | or characters, forms a pipeline. With |, the standard output of the command is redirected to the standard input of the command that follows. With &, both the standard error and output are redirected through the pipeline.

Pipelines can be separated by semicolons (;), in which case they are executed sequentially. Pipelines separated by & or | form conditional sequences in which the execution of pipelines depends on the success or failure of the left.
