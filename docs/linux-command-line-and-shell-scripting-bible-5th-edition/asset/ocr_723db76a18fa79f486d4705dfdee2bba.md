# **TABLE 6.2 The Bash Shell Environment Variables**

| Variable | Description |
| :--- | :--- |
| BASH | The full pathname to execute the current instance of the Bash shell |
| BASH_ALIASES | An associative array of currently set aliases |
| BASH_ARGC | A variable array that contains the number of parameters being passed to a subroutine or shell script |
| BASH_ARGV | A variable array that contains the parameters being passed to a subroutine or shell script |
| BASH_ARGV0 | A variable that contains the name of either the shell or, if used within a script, the shell script's name |
| BASH_CMDS | An associative array of locations of commands the shell has executed |
| BASH_COMMAND | The shell command currently being or about to be executed |
| BASH_COMPAT | A value designating the shell's compatibility level |
| BASH_ENV | When set, each Bash script attempts to execute a startup file defined by this variable before running |
| BASH_EXECUTION_STRING | The command(s) passed using the bash commands -c option |
| BASH_LINENO | A variable array containing the source code line number of the currently executing shell function |
| BASH_LOADABLE_PATH | A colon-separated list of directories where the shell looks for dynamically loadable built-ins |
| BASH_REMATCH | A read-only variable array containing patterns and their sub-patterns for positive matches using the regular expression comparison operator, =~ |
| BASH_SOURCE | A variable array containing the source code filename of the currently executing shell function |
| BASH_SUBSHELL | The current nesting level of a subsHell environment (the initial value is 0) |
| BASH_VERSINFO | A variable array that contains the individual major and minor version numbers of the current instance of the Bash shell |
| BASH_VERSION | The version number of the current instance of the Bash shell |
| BASH_XTRACEFD | If set to a valid file descriptor (0, 1, 2), trace output generated from the `set -x' debugging option can be redirected; this is often used to separate trace output into a file |
| BASHOPTS | A list of Bash shell options that are currently enabled |
| BASHPID | Process ID of the current Bash process |
| CHILD_MAX | A setting that controls the number of exited child status values for the shell to track |