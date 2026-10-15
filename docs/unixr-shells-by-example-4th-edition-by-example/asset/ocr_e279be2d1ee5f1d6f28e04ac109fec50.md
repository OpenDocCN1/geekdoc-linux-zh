# Table 12.15 Built-In Commands and Their Functions (continued)

| Command | Function |
|---|---|
| fc -e [ editor ] [ lnr ] first last | Used to edit commands in the history list. If no editor is specified, the value of FCEDIT is used; if FCEDIT is not set, /bin/ed is used. Usually history is aliased to fc -l.

**EXAMPLES**

fc -l Lists the last 16 commands on the history list.
fc -e emacs grep Reads the last grep command into the emacs editor.
fc 25 30 Reads commands 25 through 30 into the editor specified in FCEDIT, by default the ed editor.
fc -e - Re-executes the last command.
fc -e - Tom=Joe 28 Replaces Tom with Joe in history command 28.
fg Brings the last background job to the foreground.
fg %n Brings job number n to the foreground. Type jobs to find the correct job number. |
| jobs [-l] | Lists the active jobs by number and with the -l option by PID number.

**EXAMPLES**

$ jobs
[1] + Running sleep 50&
[1] - Stopped vi
[2] Running sleep&
|
| kill [-signal process ] | Sends the signal to the PID number or job number of process. See /usr/include/sys/signal.h for a list of signals.

**SIGNALS**

SIGHUP1 /* hangup (disconnect) */
SIGINT 2 /* interrupt */
SIGQUIT 3 /* quit */
SIGILL 4 /* illegal instruction (not reset when caught) */
SIGTRAP 5 /* trace trap (not reset when caught) */
SIGIOT 6 /* IOT instruction */
SIGABRT 6 /* used by abort, replace SIGIOT in the future */
SIGEMT 7 /* EMT instruction */
SIGFPE 8 /* floating-point exception */
SIGKILL 9 /* kill (cannot be caught or ignored) */
SIGBUS 10 /* bus error */
SIGSEGV 11 /* segmentation violation */
SIGSYS 12 /* bad argument to system call */
SIGPIPE 13 /* write on a pipe with no one to read it */
SIGALRM 14 /* alarm clock */
SIGTERM 15 /* software termination signal from kill */