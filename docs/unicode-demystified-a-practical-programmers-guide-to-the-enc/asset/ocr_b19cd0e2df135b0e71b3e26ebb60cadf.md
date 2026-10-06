# 514 Chapter 11 The emacs Editor

+   - Rmail: reads, archives, and composes e-mail
- Dired: moves around in an -l display and operates on files
- VIP: simulates a complete vi environment
- Shell: runs an interactive subshell from inside an emacs buffer

This discusses only Shell mode.

# Shell Mode

One-time shell commands and Region filtering were discussed earlier. Refer to “Foreground Shell Commands” on page 503. In Shell mode, however, each emacs buffer has an underlying shell permanently associated with it. This shell takes its input from the last line of the buffer and sends its output to the buffer, advancing Point as it goes. The buffer, if not edited, is a record of the complete shell session.

The shell runs asynchronously, whether or not you have your buffer in view. The emacs editor uses idle time to read the shell's output and add to the buffer.

Type Meta-x shell to create a buffer named *shell* exists, emacs just switches to that buffer. The name to run is taken from one of the following sources:

+   - The Lisp variable explicit-shell-file-name
- The environment variable SHELL
- The environment variable SHELL

If you really want to start a second shell, first use Meta-x rename-buffer to change the name of the existing shell's buffer. This process can be continued to create many subshells and buffers as you want, all running in parallel.

In Shell mode a special set of commands is defined (Table 11-21). They are bound to two-key sequences starting with CONTROL-C. Each sequence is meant to be similar to the ordinary control characters found in UNIX but with leading CONTROL-C.

| Shell Mode || table 11-21 |
| RETURN | If Point is at the end of the buffer, emacs inserts the RETURN and sends this (the last) line to the shell, If Point is elsewhere, it copies this line to the end of the buffer, peeling off the old shell prompt (see the regular expression shell-prompt-pattern), if one existed. Then this copied line, now the last in the buffer, is sent to the shell. |