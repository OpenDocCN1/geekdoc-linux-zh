+   8. Now we can use this Perl script to produce a customized Tripwire policy file:

```
# cd /etc/tripwire
# mv twpol.txt twpol.txt.orig
# /usr/local/bin/cleanpol.pl < twpol.txt.orig \ > twpol.txt
...
Number of additions: 38
Number of removals: 125
```

This little script saved us from making 163 manual changes to the Tripwire policy file! (The number of changes made on your system will vary depending on which packages you have installed.) You can review the changes that were made with the `diff` command:

```
diff twpol.txt.orig twpol.txt
```

+   9. Now, use `gedit`, or your favorite text editor, to review the contents of the updated `/etc/tripwire/twpol.txt` file. In particular, there may be a problem with the line defining the policy for `/sbin/e2fsadm`. If the `cleanpol.pl` script uncommented this line, then the note `tune2fs?` at the end of the line is treated by Tripwire as a relative path to a file, and the policy file is rejected. Simply delete this note. In other words:

```
/sbin/e2fsadm -> $(SEC_CRIT) ; tune2fs?
```

becomes:

```
/sbin/e2fsadm -> $(SEC_CRIT) ;
```

+   10. Now we have set up the Tripwire policy file, the next step is to initialize the Tripwire database. This is done by running the `twinstal.sh` script in `/etc/tripwire`:

```
# ./twinstal.sh
```

This script asks us to enter site and local passphrases (a term used to describe a long "password"), generates encryption keys and cryptographically secures the configuration and policy files to prevent unauthorized changes:

```
[root@rh9 tripwire]# ./twinstal.sh
-----------------------------------------------------------------------
The Tripwire site and local passphrases are used to
sign a variety of files, such as the configuration,
policy, and database files.

Passphrases should be at least 8 characters in length
and contain both letters and numbers.
```

522