# trap, onintr 1439

# trap, onintr — Shell Built-in Functions to Respond to Hardware Signals

# Synopsis

+   - sh
trap [argument n [n2...]]
- csh
onintr [-| label]
- ksh
* trap [arg sig [sig2...]]

# Description

Use the built-in shell trap and onintr commands in shell scripts to specify a sequence of commands to be executed when your shell script receives an interrupt signal.

# Bourne Shell

The trap argument is read and executed when the shell receives numeric or symbolic signal(s).

> Note — argument is scanned once when the trap is set and once when the trap is taken.

Trap commands are executed in order of signal number or corresponding symbolic names. Any attempt to trap a signal that was ignored entry to the current shell is ineffective. An attempt to trap on signal 11 (memory fault) produces an error. If you do not specify argument, all trap(s) n to their original values. If argument is a null string, the signal is ignored by the shell and the commands it invokes. If n is 0, the trap command is executed on exit from the shell. The trap command with no arguments prints a list of commands associated with each signal number.

# C Shell

The onintr command controls the action of the shell on interrupts. With no arguments, onintr restores the default action of the shell on interrupts.(The shell terminates scripts and returns to the terminal command input level.) With the - argument, the shell ignores all interrupts. With a label argument, the shell executes a goto label when an interrupt is received or a child process terminates it was executed.

# Korn Shell

trap uses a argument to be read and executed when the shell receives signal(s) sig.

> Note — argis scanned once when the trap is set and once when the trap is taken.

You can specify sigas a number or the name of the shell. trap commands are executed in order of signal number. Any attempt to trap a signal that was ignored entry to the current shell is ineffective. If you omit arg or it is -, then the trap(s) for each sigare reset to their original values. If argis null (the empty string "")