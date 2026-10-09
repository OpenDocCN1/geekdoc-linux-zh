host key. When HashKnownHosts (page 675) is set to yes (the default), OpenSSH hashes the system name and address for security. Because it hashes the hostname and IP address separately, OpenSSH puts two lines in known_hosts for each host. The following lines (they are two logical lines, each of which wraps on to several physical lines) from known_hosts are used to connect to a remote system using RSA (page 1170) encryption:

```
$ cat ~/.ssh/known_hosts
|1PrVUqxFVnnVLrkmq18yCmmZaZc=|TvRAtwaqjI1SEJ3g9uFR5j3f1AR8= ssh-rsa
     AAAAB3NzaCIyC2EAAAABIwAAQEAegm4Ya0Oj5/JtGULt3jqC5Rfcf8/JRAUiXk2DAqJ5fE...
|1Pnu88U9Qe7s5GWCiCIUIT18qyc5=|Ldm5/7L6K8v84d52129mnw2zj80b= ssh-rsa
     AAAAB3NzaCIyC2EAAAABIwAAQEAegm4Ya0Oj5/JtGULt3jqC5Rfcf8/JRAUiXk2DAqJ5fE...
```

You can use ssh-keygen with the -R option followed by the hostname to remove a hashed entry. The -F option to ssh-keygen displays a line in a known_hosts file that corresponds to a specified system, even if the entry is hashed:

```
$ ssh-keygen -F plum
# Host plum found: line 1 type RSA
|1PrVUqxFVnnVLrkmq18yCmmZaZc=|TvRAtwaqjI1SEJ3g9uFR5j3f1AR8= ssh-rsa
     AAAAB3NzaCIyC2EAAAABIwAAQEAegm4Ya0Oj5/JtGULt3jqC5Rfcf8/JRAUiXk2DAqJ5fE...
```

OpenSSH automatically stores keys from servers it has connected to in user-private files (~/.ssh/known_hosts). These files work only for the user whose directory they appear in. Working with root privileges and using a text editor, you can copy non-hashed lines from a user's private list of known hosts to the public list in /etc/ssh/ssh_known_hosts to make a server known globally on the local system.

The following example shows how Sam, who has administrative privileges, puts the hashed entry from his known_hosts file into the global ssh_known_hosts file. First, working as himself, Sam sends the output of ssh-keygen through tail to strip off the Host plum found line and redirects the output to a file named tmp_known_hosts. Next, working with root privileges, Sam appends the contents of the file he just created to /etc/ssh/ssh_known_hosts. This command creates this file if it does not exist. Finally, Sam removes the temporary file he created and returns to working as himself.

```
sam@dog:~$ ssh-keygen -F plum | tail -1 > tmp_known_hosts
root@dog:~$ sudo -i
root@dog:~# cat ~/sam/tmp_known_hosts >> /etc/ssh/ssh_known_hosts
root@dog:~# exit
sam@dog:~$ rm ~/sam/tmp_known_hosts
```

Because the output from cat is redirected, Sam creates a shell with root privileges (sudo -i) to execute the command. See page 424 for a discussion of redirecting the output of a command run under sudo.