+   Remove the /home/student//.ssh/known_hosts from servera. This causes ssh to lose the recorded identities of the remote systems.

```
$student@servera~$ rm /home/student/.ssh/known_hosts
```

Host keys can change for legitimate reasons: perhaps the remote machine was replaced because of a hardware failure, or the remote machine was reinstalled. Usually, it is advisable to remove the key for the particular host in the known_hosts file. Since this known_hosts file has only one entry, you can remove the entire file.

+   Open an SSH session to server as student. Accept the key if you asked. Use the password when prompted for the password of the student on server.

```
$student@server~$ student@server '172.25.250.11' can't be established.
ECDSA key fingerprint is SHA256:ERTdjooI2rwSwZQngD5or+JXfbidugubdXBuHuwZA
Are sure you want to continue connecting (yes/no) yes
Warning: Permanently added '172.25.250.11' (ECDSA) to the list of known hosts
student@servers password: student
...omitted...
[student@server~$]
```

Notice that the ssh command asked for your confirmation to accept or reject the host key because it could not find the remote host.

+   Exit the student user's shell on server and confirm that a new instance of known_hosts exists on servera.

```
$student@server~$ exit
logout
Connection to server closed.
$student@server~$ ls -l /home/student/.ssh/known_hosts
-rw-r--r-- 1 student 183 Feb 1 20:26 /home/student/.ssh/known_hosts
```

+   Confirm that the new instance of known_hosts file has the host key of servera.

```
$student@server~$ cat /home/student/.ssh/known_hosts
172.25.250.11 ecdsa-sha2-nistp256
AAAAAE2VjZHNLOkYToYTildZhNYTAAAAmIldZhNYTAAABB019LEYEhmU1rqnQBBPukH2Ba0/QBa9Wub5n4b3S3mihwKKFFFA/UNj8NDpEmHke/GmnkcEYMLbCfd9nNA=
```

Actual output.

+   Run hostname remotely on serverb without accessing the interactive shell.

```
$student@server~$ student@server hostname
student@server's password: student
server.lab.example.com
```

The preceding command displayed the hostname of the remote system serverb.