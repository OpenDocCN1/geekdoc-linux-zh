
## 610

## ksh, rksh

string. Use a string to locate the most recent command starting with the given string. Use a negative number as an offset to the current command number. If you use the -l option, list the command on standard output. Otherwise, invoke the editor program emulate on a file containing these keyboard commands. If you do not supply emulate, the value of the variable PEDIT (default /bin/ed) as the editor. When editing is complete, execute the command(s). If you do not specify list, then the command is set to first. If you do not specify first, the default is the previous command for editing and for listing. The -r option reverses the order of the commands, and the -n option supplies command numbers when listing. In the second form, the command is reexecuted after it performs the substitution old=new. If you specify no command argument, execute the most command typed at this terminal.

```
fg [%job...]
```

On systems that support job control only, bring each job specified to the foreground. Otherwise, bring the current job into the foreground. "Job Control" on page 586 for a description of the format of job.

```
getopts optname [arg...]
```

Check for legal options. If you use arg, use the positional parameters. Begin an option argument with a + or a -. An option not beginning with + or - the argument -- optstring contains the letters that getsopts recognizes. If you follow a letter by a :, that option is expected to have an argument. You can separate the options from the argument by blanks. getsopts places the next option it finds inside variable name each time it is invoked with a +. prepended when arguments have a +. The index of the next argument is stored in OPTIND. The option argument, if any, is stored in OPTARG. leading : in optstring stores the length of an invalid option in OPTARG and sets name to ? for an unknown option and to : when a required option is missing. Otherwise, getsopts prints an error message. The exit status is non-zero when there are no more options. getsoptsct(1) for usage and description.

```
hash [name...]
```

For each name, determine the location in the search path of the command specified by name, and remember it. The -r option forgets all remembered locations. If you give no arguments, present information in the hash output. Hits is the number of times a command has been invoked by the shell process. Cost is a measure of the work required to locate a command in the search path. If a command is found in a relative directory in the search path, after changing to that directory, recalculate the stored location of that command. Recalculated commands are indicated by an asterisk (*) adjacent to the Hits information. Cost is incremented when the recalculation is done.

## ksh, rksh 611

jobs [-lnp] [%job...]

List information about each given job; or, if you omit job, list all active jobs. The -l option lists IDs in addition to the normal information. The -n option lists only jobs that have stopped or exited since last notified. The -p option lists only the process group. See “Job Control” on page 586 for a description of the format of job

```
kill [-sig] %job...
kill [-sig] pid...
kill -l
```

Send either the TERM (terminate) signal or the specified signal to the specified jobs or processes. You can specify signals by number or by name (as given in signal(5)) stripped of the prefix SIG, with the exception that SIGHD is named CHILD); then you use TERM (terminate) or HUP (hangup), then the job or process is sent a CONT (continue) signal if it is stopped. The argument job can be the process ID of a process that is not a member of one the active jobs. See “Job Control” on page 586 for a description of the format of job. The third form, kill -1, lists the signal names.

let arg... Each is a separate arithmetic expression to be evaluated. The exit status is 0 if the value of the last expression is non-zero, and 1 otherwise.

login argument... Equivalent to exec login argument.... See login(1) for usage and description.

- * newgrp [arg...] Equivalent to exec /bin/newgrp arg...

print [-Rnprsu[n]] [arg...] The shell output mechanism. With no options or option - or -- print the arguments on standard output as described by echo(1). The exit status is 0, unless the output file is not written to.

- -n The arguments are not followed by a newline.
- -R The arguments are printed backwards.
- -p The arguments are printed with the process ID.
- -r The arguments are printed in reverse.
- -s The arguments are printed with escape sequences.
- -u The arguments are printed in uppercase.
- -n The arguments are not followed by a newline.
- * The output is the current working directory.

pwd Equivalent to the current working directory.

## 641

## ksh, rksh

```
read [-prsu[n]] [arg...] [name]
```

Read commands, and check them for syntax errors, but do not execute them. Ignored for interactive shells.

```
set [abCefhkmnopstuvwx] [+ option]... [± name]
```

The options for this command have as follows:

- -A Unset variable name
- -a Automatically export all variables that are defined.
- -b Notify the user asynchronously of job completions. The following message is written to error:
```
"%d%c %s\n", job-number, current, status, job-name
```

## 642

## ksh, rksh

current The + character identifies the job that would be used as a default for the fg or bg commands. You can also specify this job with the job-number%. The - character identifies the job that would become the default if the current job were to exit. You can also specify this job with the job-id-. For other jobs, this field is a space character. If there any suspended job, the current job is a suspended job. If there are at least two suspended jobs, the previous job is also a suspended job.

- job-name Unspecified. When the shell notifies the user that a job has been completed, it may remove the job's process ID from the list of those known in the shell execution environment. Asynchronous notification is not enabled by default.

- job-number A number used to identify the process group to the wait, fg, bg, and kill commands. Using these commands, you can identify the job by prefixing the job number with %.

- status Unspecified.

- C Prevent existing files from being overwritten by the shell's redirection operator, the > redirection operator overrides this noclobber option for an individual file.

- e If a command has a non-zero exit status, execute the ERR trap if set, and exit. This mode is disabled while profiles are read.

- f Disable file-name generation.

- h Make each command a tracked alias as first encountered.

- k Put all variable assignment arguments in the environment for a command, not just those that precede the command

- m Run background jobs in a separate process group, and print a line on completion. Report the exit status of background jobs in a completion message. On systems with job control, this option is turned on automatically for interactive shells.

- n Read commands, and check them for syntax errors, but do not execute them. Ignored for interactive shells.

- o The argument for this option can be one of the following names:

- alexport Same as -a.
