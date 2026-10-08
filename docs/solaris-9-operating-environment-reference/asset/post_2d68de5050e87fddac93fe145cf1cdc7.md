
# stty 1355

```
saveterm="$(stty -g)    # save terminal state
stty (new settings)         # set new state
#                             # ...
stty $saveterm               # restore terminal state
```

Because the -a format is loosely specified, scripts that save and restore settings should use the -g option.

# Examples
The following example shows the output from the stty command when no options are specified.

```
castle$ stty
ispeed 89376 baud; ospeed 89360 baud; -parity cstopb hupcl loblk
rows = 37; columns = 80; ypixels = 491; xpixels = 570;
quit = <undef>; erase = #hw; switch = <undef>
-inpck -istrip icnl -ixany ixoff onlcr
echo echo echoe echochtl iexten
cast$
```

# Environment Variables
See environ(5) for descriptions of the following environment variables that affect the execution of stty: LC_CTYPE, LC_MESSAGES, and NLPATH.

# Exit Status
0 Successful completion.
>0 An error occurred.

# Attributes
See attributes(5) for descriptions of the following attributes:

```
/usr/bin/stty
Attribute Type    Attribute Value
Availability       SunWxcsu
```

```
/usr/xpg4/bin/stty
Attribute Type    Attribute Value
Availability       SunWxcu4
```

# See Also
tabs(1), ioctl(2), write(2), getwidth(3C), attributes(5), environ(5), ldterm(7M), termio(7I), termiox(7I)

# 1356

# sum — Print Checksum and Block Count for a File

# Synopsis

```
/usr/bin/sum [-r] [file...]
/usr/ucb/sum [file...]
```

# Description
The command calculates and prints a 16-bit checksum for the named file and the number of 512-byte blocks in the file. It is typically used to look for bad spots or to validate a file communicated over some transmission line.

Portable applications should use checksum(1).

> Note — sum and /usr/ucb/sum (see sum(1)) return different checksums.

# Options
- -r an alternative (machine-dependent) algorithm in computing the checksum.

# Operands
- file a path of a name of file. If you specify no files, use the standard input.

# Examples
The following example displays a checksum for the file kookaburra-1.

```
castle% sum kookaburra-1
23823 1 kookaburra-1
castle%
```

# Usage
largefile(5) for the description of the behavior of sum when encountering greater than or equal to 2 Gbytes(** 31 bytes**).

# Environment Variables
environ(5) for descriptions of the following environment variables that affect the execution of sum: LC_TYPE, LC_MESSAGES, and NLPATH.

# Exit Status
- 0 Successful completion.
>0 An error occurred.

# sun

# Attributes
See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNmesu |
| CSI | Enabled |

# See Also
cksum(1), sum(1B), wc(1), attributes(5), environ(5), largefile(5)

# Diagnostics
Read error is indistinguishable from end-of-file on most devices; check the block count.

# sun — Get Processor Type Truth Value

# Synopsis
/usr/bin/sun

# Description
See machid(1).

# suspend — Shell Built-in Function to Halt the Current Shell

# Synopsis
- - sh, csh, and ksh
- suspend

# Description
Bourne and Korn Shell
Stops the execution of the current shell (but not if it is the login shell).

C Shell
Stop the shell in its tracks as if it had been sent a stop signal with ^Z. This function is most used to stop shells started by su.

# Attributes
See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNmesu |

# 1358

# See Also
```
csh(1), kill(1), ksh(1), sh(1), su(1M), attributes(5)
```

# symorder — Rearrange a List of Symbols

# Synopsis
```
/usr/ccs/bin/symorder [-s] objectfile symbolfile
```

# Description
The symorder command was used in SunOS 4, specifically to cut down on the overhead of getting symbols from vunix. This command is no longer applicable because kernel symbol entries are dynamically obtained through /dev/ksym.

This script is provided as a convenience for software developers who need to maintain scripts that are portable across a variety of operating systems.

# Exit Status
symorder has exit status 0.

# Attributes
See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWtool |

# See Also
```
nlist(3E), attributes(5), ksyms(7D)
```

# sysV-make — Maintain, Update, and Regenerate Groups of Programs

# Synopsis
```
/usr/lib/svr4.make [-f makefile] [-eikrst] [names]
```

# Description
The sysV-make command is the vanilla version of make. If the environment variable USVR4_MAKE is set, then the make command invokes this version of make enables the programmer to maintain, update, and regenerate groups of computer programs (are typically programs). Source Code Control (SCCS) files.makefile, and s.makefile are tried in order. If you do not specify the -f option, then standard input is taken.

# sysV-make
make updates a target only if its dependents are newer than the target. Prerequisite files of a target are added recursively to the list of targets. Missing files are deemed outdated. You can include the directives from the following list in makefile to extend options. The directives used in makefile as if they were targets:

- DEFAULT: If a file must be made but there are no explicit commands or built-in rules, use the commands associated with the name.
- IGNORE: Same as the -i option.
- PRECIOUS: Do not remove dependents of the PRECIOUS entry when quit is pressed.
- SILENT: Same as the -s option.
> Note - Some commands return status inappropriately; use -i or a dash (-) command-line prefix to overcome the difficulty. File names containing the characters :, and @ do not work. Commands that are directly executed by the shell, notably cd(1), are ineffective across newlines in make.

# Options
- - e: Environment variables override assignments within makefiles.
- f makefile: Specify the name of file.
- i: Ignore error codes returned by invoked commands.
- k: Abandon work on the current entry if fails, but continue on other branches that do not depend on that.
- n: Print commands, but not execute them. Print line even if they begin with @.
- q: Print the complete set of macro definitions and target descriptions whether the target file has been updated. make returns 0 or non-zero status code.
- r: Do not use built-in rules.
- s: Do not print command lines before execution.
- t: Touch the target files (updating them) instead of issuing the usual commands.

# Creating the make
The make invoked with the -f option is a carefully structured file of instructions for updating and regenerating programs. It contains a sequence of entries that specify dependencies. The first line of an entry is a blank-separated, non-null list of targets, then a ; then a (possibly null) list of prerequisite files or dependencies. The following ; and all following lines with a Tab are shell commands to executed to update the target. The first nonempty line that does not begin with a Tab begins a new dependency or macro definition. You can continue shell commands across lines with a backslash-newline sequence. Everything printed by make (except the initial Tab) is passed directly to the shell as is. Thus, the following sequence

```
echo a\nb
```

produces

```
ab
```

exactly as the shell would. Number sign (#) and newline surround comments including \-newline sequences. The following Makefile says pgm depends on two files, a.o and b.o, and that they, in turn, depend on their corresponding source files (a.c and b.c) and a common file incl.h.

# 1360
make
Command lines are executed one at a time, each by its own shell. You can use the SHELL environment variable to specify which make should use to execute commands. The default is /usr/bin/sh. The first or two characters in a command can be @, -, or -. If @ is present, printing of the command is suppressed. If a - makes a line is printed if it is executed unless you spec the -s option, entry .SILENT is included in Makefile, or the initial character sequence contains a dash. The -n option specifies printing without execution; however, if the command has the string $(MAKE) in it, the line is always executed (see the discussion of the MADEOPTIONS macro in "make Environment" (page 1360)).
-t (touch) option updates the modified date of a file without executing any commands.

Commands returning non-zero status normally terminate make. If you specify the -i option, the IGNORE variable is included in Makefile, or if the initial character of the command contains a dash (-), the error is ignored. If you specify the -k option, work is abandoned on the current entry but continues on other branches that depend on that.

Interrupt and quit delete the target unless the target is a dependent of the directive PRECIOUS.

# make Environment
The environment is read by make. All variables are assumed to be macro definitions and processed as before any Makefile after the internal rules; thus, make assignments in a Makefile override environment variables. The -e option overrides the assignments in a Makefile. Suffixes and their associated rules in the Makefile override any identical suffixes in the built-in rules.
The Environment variable is processed by make as containing any legal input option (except -f and -p) defined for the command line. Further, on invocation, make "vars" works if it is not in the environment, which puts the options into it passes it on to invocations of commands. Thus, MAKEFLAGS always contains the
