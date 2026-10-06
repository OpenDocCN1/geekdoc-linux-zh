# Chapter 34. Miscellany

> Nobody really knows what the Bourne's grammar is. Even examination of the source code is little help.

Tom Duff

# 34.1. Interactive and non-interactive shells and scripts

An *interactive* shell reads commands from user input on a *tty*. Among other things, such as a shell reads startup files on activation, directs a prompt, and enables job control by default. The user can *interact* with the shell.

A shell running a script is always a non-interactive shell. All the same, the script can still access its *tty*. It is possible to eliminate an interactive shell in a script.

```
#!/bin/bash
MY_PROMPT='$'
while
  echo -n "$MY_PROMPT"
  read line
  eval "$LINE"
done
```

# This example script, and much of the above explanation supplied by
# Stephanie Chazelas (thanks again).

Let us consider an *interactive* script one that requires input from the user, usually with [read] statements (see [Example 11-2]). "Real life is actually a bit messy than that. For now, assume an interactive script is bound to a tty that a user has invoked from the console or an xterm.

Input start scripts are necessarily non-interactive, they must run without human intervention. Many administrative and system maintenance scripts are likewise non-interactive. Repetitive tasks cry out for automation by non-interactive scripts.

Non-interactive scripts can run in the background, but otherwise one hang, waiting for input that never comes. Handle that by having an *expect* script or embedded [here document] feed input to an interactive script running as a background job. In the simplest case, redirect a file to supply to the *read* statement (*read variable*). These particular workarounds make general purpose scripts that run in either interactive or non-interactive modes.

If a script needs to test whether it is running in an interactive shell, it is simply a matter of finding whether the prompt variable, [PS1] is set. (If the user is being prompted for input, then the script needs to display a prompt).

```
if [ -z $PS1 ]; then no prompt?
then
```