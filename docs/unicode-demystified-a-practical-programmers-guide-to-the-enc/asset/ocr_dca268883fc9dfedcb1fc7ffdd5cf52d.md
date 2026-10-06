replicate complicated commands and arguments that you used earlier in this login session or in a previous one and enter a series of commands that differ from one-other in minor ways. The history list is also useful as a record of what you have done. It can be helpful when you have made a mistake and are not sure what you did or when you want to keep a record of a procedure that involved a series of commands. The history building displays your history list. If it does not, read on; you need to set some variables.

The TC Shell and the Z Shell's history mechanisms are similar to bash's have some important differences. In addition to the following sections, see page 686 and 795

# history Can Help Track Down Mistakes

When you have made a command line mistake (not an error in a script or program) and are not sure what you did, you can look at the history list to review your recent commands. Sometimes this list can help you figure out what went wrong and how to fix things.

The value of the HISTSIZE variable determines the number of events preserved in the history list during a session. Although the default value for HISTSIZE 500, you may want to set it to a more convenient value, such as 100.

When you exit the shell, the most recently executed commands are saved in the file given by the HISTFILE variable (the default is .bash_history) in your home directory. The next time you start up the shell, it initializes the history list. The value of the HISTFILE variable (default 500) determines the number of lines of history saved in HISTFILE (not necessarily the same as HISTSIZE). HISTSIZE holds the number of events remembered during a session, HISTFILE holds the number remembered between sessions, and file designated by HISTFILE holds the name of the file that holds the history list. See Table 12-3

# History Variables

| Function | Variable | Default |
|---|---|--|
| Maximum number of events saved during a session | HISTSIZE | 500 events |
| Location of the history file | HISTFILE | ~/.bash_history |
| Maximum number of events saved between sessions | HISTFILE | 500 events |