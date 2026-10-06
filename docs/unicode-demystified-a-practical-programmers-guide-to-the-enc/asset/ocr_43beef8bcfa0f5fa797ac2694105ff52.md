# echo

Displays a message
echo [options] message
The echo utility copies its arguments, followed by a NEWLINE, to standard output. Each of the shells has an echo builtin that works similarly to the echo utility.

# Arguments

The message is one or more arguments, which can include quoted strings, ambiguous file references, shell variables. A SPACE separates each argument from the others. The shell recognizes special characters in the arguments, for example, the shell expands an asterisk into a list of filenames in the working directory.

# Options

+   -n Suppresses the NEWLINE terminating the message
-e Enables the interpretation of backslash-escaped characters
-E Suppresses the interpretation of backslash-escaped characters (default).
--help Gives a short summary of how to use echo. The summary includes a list of the escape sequences interpreted by echo. Works only with echo utility (/bin/echo) and not with the echo builtin

# Notes

You can use echo to send messages to the screen (refer to Chapter 12). For other uses of echo, see the discussion of echo starting on page 158.
The echo utility and builtins provide an escape notation to represent certain non-printing characters in message you must use the -e option to get these sequences to work with the echo utility and builtin. Do not use the -e option with the echo builtin. Refer to the Optional Section on page 781 if you are using the \c escape sequence or the -n option to suppress a trailing NEWLINE in zsh.

# Examples

The following examples show how the echo command can be used:
Secho "This echo command has one argument."
This echo command has one argument.