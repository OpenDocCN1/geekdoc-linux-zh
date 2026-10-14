Output files must be writable. If you are uncertain about the permission status of a specific target output file, direct the results of the command to the /usr/spool/uucppublic directory; ~uucp is a brief way of specifying this directory from a shell.

# 14.4.1 Using uux from the Bourne, Korn, or POSIX Shells

The following example shows how the uux command uses the operating system cat command to concatenate the /u/doc/F1 file located on host gem, with the /usr/doc/F2 file located on host sky. The result is placed in the /u/doc/F3 file on host gem.

```
uux "gem!cat gem!/u/doc/F1 sky!/usr/doc/F2 > gem!/u/doc/F3"
```

In the following example, the task is the same as in the previous command, but braces ({ }) are used instead of the redirection symbol to specify the destination in the uux command line. The task is the same as in the previous command, but the destination output is implicit:

```
uux gem!cat gem!/u/doc/F1 sky!/usr/doc/F2 \{gem!/u/doc/F3\}
```

# 14.4.2 Using uux from the C Shell

To perform the same operation as in the previous section, but in the C shell, enter one of the following uux commands:

```
uux "gem\!cat gem\!/u/doc/F1 sky\!/usr/doc/F2 > gem\!/u/doc/F3"
```

The following example uses an implicit destination output file:

```
uux gem\!cat gem\!/u/doc/F1 sky\!/usr/doc/F2 \{gem\!/u/doc/F3\}
```

In the two following examples, uux uses the cat command to send the acct6 file from remote host boston, as output to the acct6 file in the public directory on your local host:

```
uux "cat boston\!/reports/acct6 > ~uucp/acct6"
```

The following example uses an implicit destination output file:

```
uux cat  boston\!/reports/acct6 \{~uucp/acct6\}
```

# 14.4.3 Other uux Features and Suggestions

The uux command assumes your local host is the default, so you do not need to specify it in the command line. For example, to run the diff command to compare the /u/F1 file on host car with the /u/F2 file on host sea, and place the result in the /u/F3 file on the local host, use the following command:

```
uux "diff  car!/u/F1  sea!/u/F2  >  /u/F3"
```