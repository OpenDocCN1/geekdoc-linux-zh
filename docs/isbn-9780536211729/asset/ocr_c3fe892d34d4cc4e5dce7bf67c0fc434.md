```
diff $ /etc/$si >> .tmp$
  echo "----------------" >> .tmp$$
```

```
endif
if (-f .tmp$$) then
  Mail -s 'NOT OK: /etc conf analysis' \
    $* < .tmp$$
  /bin/rm .tmp$$
  exit 1
else
  echo "All ok" \
  Mail -s 'ok:/etc conf analysis' $*\n  exit 0
endif
```

# 8.19 Tripwire

root note accounts in /etc/passwd with a UID of 0 with variations on "root": "door" and "root" are entries. With plus signs ('+') are common too. These are frequently found at the end or in the middle of /etc/passwd. .hosts .equiv files, are popular on systems where the SysAdmin has not yet disabled rsh and friends, as discussed in "Turn Off rsh, rpc, login, and reexec" on page 94, or when ssh is allowed to use these files. For suspicious entries in /etc/hosts,/etc/hosts.allow, and /etc/hosts.deny /etc/aliases file, used by sendmail, also be used for root exploits because it can be used to arrange for e-mail to a particular name to cause the execution of any program as root to process recipient’s e-mail.

Tripwire is a powerful tool that computes a hard-to-fake MD5 checksum of each file on your system that you are interested in monitoring for tampering (Trojan horses, altered or deleted data, etc.). These would include your system configuration files in /etc, system programs in /bin and /usr/bin, applications, and user accounts. At any subsequent time, you can ask Tripwire to recompute these checksums and inform you of any changes from the previously computed baseline. By knowing usage patterns in your system, you easily decide which changed files are likely to be legitimate, such as /home/joe/mbox, and