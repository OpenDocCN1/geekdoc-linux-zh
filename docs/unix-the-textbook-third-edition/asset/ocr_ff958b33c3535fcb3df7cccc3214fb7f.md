```
$ ls -l cp.new foo
-rwSr--r-- 1 sarwar faculty 14 Aug 4 23:38 cp.new
-r-sr-xr-x 1 sarwar faculty 30 Aug 5 05:27 foo
$
```

The chmod command with the following syntax may be used to set the SUID bit.

# SYNTAX

```
chmod 4xxx file-list
chmod u+s file-list
```

Purpose: Change/set the SUID bit for files in file-list

Here, xxx is the octal number that specifies the read, write, and execute permissions for user, group, and others, and the octal digit 4 (binary 100) is used to set the SUID bit. When the SUID bit is set, the execute bit for the user is set to s (lowercase) if the execute permission is already set for the user; otherwise, it is set to S (uppercase). The following session illustrates the use of these command syntaxes. The first, the ls -l cp.new command, is used to show that the execute permission for the cp.new file is set. The chmod 4710 cp.new command is used to set the SUID bit and other nine bits of permission to octal 710. The second, the ls -l cp.new command, shows that the x bit value has changed to s. The two subsequent chmod commands are used to set the SUID and execute bits to 0. The ls -l cp.new command is used to show that execute permission has been taken away from the owner. The chmod u+s cp.new command is used to set the SUID bit again, and the last ls -l cp.new command shows that the bit value is S (uppercase) because the execute bit was not set prior to setting the SUID bit.

```
$ ls -l cp.new
-rwX--x-- 1 sarwar faculty 14 Aug 4 23:26 cp.new
$ chmod 4710 cp.new
$ ls -l cp.new
-rws--x--- 1 sarwar faculty 14 Aug 4 23:26 cp.new
$ chmod u-s cp.new
$ chmod u-x cp.new
$ ls -l cp.new
-rw----x-- 1 sarwar faculty 14 Aug 4 23:26 cp.new
$ chmod u+s cp.new
$ ls -l cp.new
-rwS--x--- 1 sarwar faculty 14 Aug 4 23:26 cp.new
$
```

Although the idea of the SUID bit is sound, it can compromise the security of the system if not implemented correctly. For example, if the permissions of any set-UID program are