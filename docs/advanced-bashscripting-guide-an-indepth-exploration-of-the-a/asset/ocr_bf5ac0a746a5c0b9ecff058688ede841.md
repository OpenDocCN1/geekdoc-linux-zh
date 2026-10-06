# Advanced Bash–Scripting Guide

The source for a number of load builtins is typically found in the /usr/share/doc/bash-??/functions directory.

Note that the -f option to enable is not portable to all systems.

+   [28] The same effect as autoload can be achieved with typeset -fu.

+   [29] These are files named with a dot, such as ~.Defaults. Such filenames do not show up in a normal listing, and cannot be deleted by an rm -rf *.Dotelfaults are generally used as setup and configuration files in a user's home directory.

+   [30] A tar cvzf will include directories below the current working directory. This is an undocumented tar "feature".

+   [31] This is a symmetric block cipher, to encrypt files on a single system or local network, as opposed to the "public key" cipher class, of pgp is a well-known example.

+   [32] A daemon is a background process not attached to a terminal session. Daemons perform designated services either when triggered or explicitly by certain events.

The word "daemon" means ghost in Greek, and there is certainly something mysterious, almost supernatural, about how the UNIX daemons silently wander behind the scenes, carrying out their appointed tasks.

+   [33] This is actually a script adapted from the Debian distribution.

+   [34] The print queue is the group of jobs "waiting in line" to be printed.

+   [35] For an excellent overview of this topic, see Andy Vaught's article, Introduction to Named Pipes, in the September, 1997 issue of Linux Journal.

+   [36] EBCDIC (pronounced "ebcd-sid-ic") is an acronym for Extended Binary Coded Interchange Code. It is an IBM data format no longer in use. A bizarre application of the conv_ebcdic option of dd is a 'quick n' but not very useful text file encoder.

```
cat $file dd=swab,ebcdic > $file_encrypted
# Encode (looks like gibberish)
# Might as well switch bytes (swab), too, for a little extra orthodoxy
 $file_encrypted dd=swab,ascii > $file_plaintext
# Decode.
```

+   [37] A macro is a symbolic constant that expands into a command string or a set of operations on parameters.

+   [38] This is the case on a Linux machine or a UNIX system with disk quotas.

+   [39] The userdel command will fail if the particular user being deleted is still logged on.

Appendix J. Copyright