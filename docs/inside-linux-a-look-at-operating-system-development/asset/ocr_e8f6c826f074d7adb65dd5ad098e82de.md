to preface the variable name.

These variables exist in two domains—the first is local to the shell and the other is part of a global environment common to this process and all child processes. Local variables are inherited only by child shells. The global environment is outside of the shell and is inherited by any kind of process started by the shell. The shell looks for a variable definition first in the local environment and then in the global environment. Some of the shell variables are automatically set by the shell, others are set through explicit commands. All global variables are set through explicit commands.

For example, every time a child process completes execution, the C shell variable accessed as $status is set to indicate success or failure of that process. (The Bourne shell addresses this status variable as $?.) The shell variable notify is explicitly set by a command in the shell start-up file. The global variable HOSTNAME has the value grieg.seaslug.org on my system.

# Control of execution

Most shells provide methods to control the order of execution. In this respect, they are considered to support a proper programming language.

# Sequencing and Grouping   To begin with, these shells use a special token, usually “;”, to separate multiple commands on a single command line. The semantics are that the command to the left of the “;” is executed and then the command to the right of the “;” is executed. Parenthesis can be used to group commands so that they are treated as a single command by other parts of the command line.

For example, when the example on page 41 is decoded, date sees its own name as the only argument and echo sees its own name as the initial argument and “hello world” as the next argument. Neither command sees the parenthesis nor the redirection as any part of its arguments. The parentheses tell the shell that the redirection is to be applied to each of the commands.

Other tokens, described below, not only separate commands on a line, but describe additional actions to be performed by the shell.