
## BatchMode
## BindAddress
## CanonicalDomains
## CanonicalizeFallbackLocal
## CanonicalizeHostname
## CanonicalizeMaxDots
## CanonicalizePermittedCNAMEs
## ChallengeResponseAuthentication
## CheckHostIP
## Cipher
## Ciphers
## Compression
## CompressionLevel
## ConnectionAttempts
## ConnectTimeout
## ControlMaster
## ControlPath
## ControlPersist
## GlobalKnownHostsFile
## GSSAPIAuthentication
## GSSAPIDelegateCredentials
## HashKnownHosts
## Host
## HostbasedAuthentication
## HostbasedKeyTypes
## HostKeyAlgorithms
## HostKeyAlias
## Hostname
## IdentityFile
## IdentitiesOnly
## IPQoS
## KbdInteractiveAuthentication
## KbdInteractiveDevices
## KexAlgorithms
## LogLevel
## MACs
## NoHostAuthenticationForLocalhost
## NumberOfPasswordPrompts
## PasswordAuthentication
## PKCS11Provider
## Port
## PreferredAuthentications
## Protocol
## ProxyCommand
## PubkeyAcceptedKeyTypes
## PubkeyAuthentication
## RekeyLimit
## RhostsRSAAuthentication
## RSAAuthentication
## SendEnv
## ServerAliveInterval
## ServerAliveCountMax
## StrictHostKeyChecking
## TCPKeepAlive
## UpdateHostKeys
## UsePrivilegedPort
## User
## UserKnownHostsFile
## VerifyHostKeyDNS

### -P port
Specifies the port to connect to on the remote host. Note that this option is written with a capital ‘P’ because -p is already reserved for preserving the times and modes of the file.

### -p
Preserves modification times, access times, and modes from the original file.

### -q
Quiet mode: disables the progress meter as well as warning and diagnostic messages from ssh(1).

### -r
Recursively copy entire directories. Note that scp follows symbolic links encountered in the tree traversal.

### -S program
Name of program to use for the encrypted connection. The program must understand ssh(1) options.

### -v
Verbose mode. Causes scp and ssh(1) to print debugging messages about their progress. This is helpful in debugging connection, authentication, and configuration problems.

## EXIT STATUS

Exit status of scp.

## SEE ALSO

scp(1), ssh(1), ssh-add(1), ssh-agent(1), ssh-keygen(1), ssh_config(5), scp(8)

## HISTORY

scp is based on the rcp program in BSD source code from the Regents of the University of California.

## AUTHORS

Timo Rinne and Tatu Ylonen.

## SCRIPT

## NAME

script - make typescript of terminal session

## SYNOPSIS

```
script [options] [file]
```

## DESCRIPTION

script makes a typescript of everything displayed on your terminal. It is useful for students who need a hardcopy record of an interactive session as proof of an assignment, as the typescript file can be printed out later with a2ps(1).

If the argument file is given, script saves the dialogue in this file. If no filename is given, the dialogue is saved in the file typescript.

## OPTIONS

- **-a, --append**
  Append the output to file or to typescript, retaining the prior contents.

- **-c, --command command**
  Run the command rather than an interactive shell. This makes it easy for a script to capture the output of a program that behaves differently when its stdout is not a tty.

- **-e, --return**
  Return the exit code of the child process. Uses the sa format as bash termination on signal termination exit code is `128+n`.

- **-f, --flush**
  Flush output after each write. This is nice for telecooperation: one person does `mkfifo foo; script -f foo`, and another can supervise real-time what is being done using `cat foo`.

- **--force**
  Allow the default output destination, i.e. the typescript file, to be a hard or symbolic link. The command will follow a symbolic link.

- **-q, --quiet**
  Be quiet (do not write start and done messages to either standard output or the typescript file).

- **-t, --timing[=file]**
  Output timing data to standard error, or to file when given. This data contains two fields, separated by a space. The first field indicates how much time elapsed since the previous output. The second field indicates how many characters were output this time. This information can be used to replay typescripts with realistic typing and output delays.

- **-V, --version**
  Display version information and exit.

- **-h, --help**
  Display help text and exit.

## NOTES

The script ends when the forked shell exits (a control-D for the Bourne shell (sh(1)), and exit, logout or control-d (if ignoreeof is not set) for the C-shell, csh(1)).

Certain interactive commands, such as less(1), create garbage in the typescript file. script works best with commands that do not manipulate the screen, the results are expected to relate to a hardcopy terminal.

It is not recommended to run script in non-interactive shells. The inner shell of script is always interactive, and this could lead to unexpected results. If you use script in the shell initialization file, you have to avoid entering an infinite loop. Use e. g. profile file, which is read by login shells only:

```
if test -t 0 ; then script exit fi
```

You should also avoid use of script in command pipes, as script can read more input than you would expect.

## ENVIRONMENT

The following environment variable is utilized by script:

- **SHELL**
  If the variable SHELL exists, the shell forked by script will be that shell. If SHELL is not set, the Bourne shell is assumed. (Most shells set this variable automatically).

## SEE ALSO

a2ps(1) (for the history mechanism), csh(1).

## HISTORY

The script command appeared in 3.0BSD.

## BUGS

script places everything in the log file, including linefeeds and backspaces. This is not what the naive user expects.

script is primarily designed for interactive terminal sessions, it’s possible that when stdin is not a terminal (for example “echo foo | script”) then all session hangs up, because interactive shell within script session misses EOF and the script has no clue when to close the session. See the NOTES section for more information.

## AVAILABILITY

The script command is part of the util-linux package and is available from Linux Kernel Archive

## SCRIPTREPLAY

## NAME

scriptreplay - play back typescripts, using timing information

## SYNOPSIS

scriptreplay [options] [-t] timingfile [typescript [divisor]]

## DESCRIPTION

This program replays a typescript, using timing information to ensure that output happens in the same rhythm as it originally appeared when the script was recorded.

The replay simply displays the information again; the programs that were run when the typescript was being recorded are not run again. Since the same information is simply being displayed, scriptreplay is only guaranteed to work properly if run on the same type of terminal the typescript was recorded on. Otherwise, any escape characters in the typescript may be interpreted differently by the terminal to which scriptreplay is sending its output.

The timing information is what script(1) outputs to standard error if it is run with the -t parameter.

By default, the typescript to display is assumed to be named typescript, but other filenames may be specified, as the second parameter or with option -s.

If the third parameter is specified, it is used as a speed-up multiplier. For example, a speed-up of 2 makes scriptreplay go twice as fast, and a speed-up of 0.1 makes it go ten times slower than the original session.

## OPTIONS

The first three options will override old-style arguments.

- **-t, --timing file**
  File containing script's timing output.

- **-s, --typescript file**
  File containing script's terminal output.

- **-d, --divisor number**
  Speed up the replay displaying this number of times. The argument is a floating point number. It's called divisor because it divides the timings by this factor.

- **-m, --maxdelay number**
  Set the maximum delay between transcript updates to number of seconds. The argument is a floating point number. This can be used to avoid long pauses in the transcript replay.

- **-V, --version**
  Display version information and exit.

- **-h, --help**
  Display help text and exit.
