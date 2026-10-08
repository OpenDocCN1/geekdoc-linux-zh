# tset, reset 1453

! It is not the case that. (Negates the above operators.)

? Prompt for the terminal type. If no response is given, then types selected by default.

In the following example, the terminal type is set to adm3a if the port is a dialup with a speed greater than 300 or to dv2 if the port is a dialup at 300 baud or less. In the third case, the question mark preceding the terminal type means that you are to verify the type desired. A null response indicates that the named type is correct. Otherwise, your response is taken to be the type desired.

```
tset -m 'dialup:300:adm3a' -m
'dialup:dv2' -m \
'plugboard?adm3a'
```

To prevent interpretation as metacharacters, enclose the entire argument to -m in single quotes. When using the C shell, precede explanation points by a backslash (\).

Specify that the new tty driver modes should be initialized for this terminal. Probably useless sty new is the default.

Suppress the Erase set and Kill set to messages.
In addition to other commands, report the terminal type.

Output commands to set and export TERM. This option can be used with
set noglob
eval 'tset -s...'
unset noglob

to bring the terminal information into the environment. Doing so makes programs such as vi(1) start faster. If the SHELL environment variable ends with csh, output C shell commands; otherwise, output Bourne commands.

# Examples

These examples use all the dash (-) option. A use of tset in a .profile or .login also uses the -e and -k options, and often the -n or -Q options as well. These options have been omitted to keep the examples short.

To select a 2621, you might put the following sequence of commands in your .login (or .profile for Bourne shell users).

```
set noglob
eval 'tset -s 2621'
unset noglob
```

If you have a switch that connects to various ports (making it impractical to identify which port you be connected to) and use virtual terminals from time to time, you can select from those terminals according to the speed or baud rate. In the example below, tset prompts you for a terminal type if the baud rate is greater than 1200 (say, 9600 for a terminal connected by an RS-232 line), and uses a Wyse by 50 for default. If the baud rate is less or equal to 1200, tset selects a 2621. Note the placement of the question mark and to protect the characters and ? from interpretation by the shell.