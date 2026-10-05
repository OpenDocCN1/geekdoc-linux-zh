+   5. Create a tar archive named /tmp/log.tar contains the contents of /var/log on serverb. Remotely transfer the tar archive to the directory /tmp/servera, authenticating using student /home/student/.ssh/server3_key as the student user's private key using the SSH key for authentication.

+   5.1. Use the sudo tar command to create another archive named /tmp/log.tar as the superuser containing the contents of /var/log.

```
[@serverb ~]$ sudo tar -cvf /tmp/log.tar /var/log
[sudo] password for student: student
...output omitted...
```

+   5.2. Use the scp command to remotely transfer the archive file /tmp/log.tar to the directory /tmp on servera. Specify /home/student/.ssh/server3_key as the private key of the SSH key pair.

```
[@serverb ~]$ scp -i .ssh/server3_key /tmp/log.tar servera:/tmp
log.tar 100% 14MB 57.4MB/s 00:00
```

+   6. Configure the rsyslog service on serverb to log all messages that receives the priority level of debug or higher to the /var/log/grading-debug. This configuration should be set in the /etc/rsyslog.d/grading-debug.conf file which you should create.

+   6.1. Create the file /etc/rsyslog.d/grading-debug.conf with the following content. You may use the sudo vim /etc/rsyslog.d/grading-debug.conf to create the file.

```
*.debug /var/log/grading-debug
```

+   6.2. Use the sudo systemctl command to restart the rsyslog service.

```
[@serverb ~]$ sudo systemctl restart rsyslog.service
```

+   6.3. Use the logger command to generate the log message Debug Testing having priority debug.

```
[@serverb ~]$ sudo logger -p debug Debug Testing
```

+   6.4. Confirm that the log message Debug Testing is saved in the /var/log/grading-debug file.

```
[@serverb ~]$ sudo tail /var/log/grading-debug
...Output omitted...
Mar 12 09:55:22 serverb student [32383]: Debug Testing
```

+   7. Use the yum command to install the ssh package, available in the BaseOS repository, on serverb.

```
[@serverb ~]$ sudo yum install zsh
...output omitted...
Is this ok [y/n]: y
```