
- Configure the rsyslog server to log all messages it receives that have the priority level of debug or higher to the file /var/log/grading-debug. This configuration should be set in /etc/rsyslog.d/grading-debug.conf file, which you need to create.
- Install the zsh package, available in the BaseOS repository, on serverb.
- Enable the default module stream for the module python36 and install all provided packages from stream on serverb.
- Set the time zone of server to Asia/Kolkata.

## 1. Generate SSH keys for the user student on serverb. Do not protect the private key with a passphrase.

### 1.1. From workstation, open an SSH session to serverb as student.

```
student@workstation ~/ ssh student@serverb
...output omitted...\
student@serverb ~
```

### 1.2 Use the ssh-keygen command to generate the SSH keys for the user student. The private and public key files should be named /home/student/.ssh/review3_key and /home/student/.ssh/review3_key.pub respectively.

```
student@serverb ~ ssh-keygen
Generating public/private rsa key
Enter file in which to save the key (/home/student/.ssh/id_rsa): /home/student/.review3_key
Enter passphrase (empty for no password): Enter
Enter same passphrase again: Enter
Your identification has been saved in /home/student/.ssh/review3_key.
Your public key has been saved in /home/student/.ssh/review3_key.pub.
SHA256:Uqfeh+VRfm4fQDbz/6IfYNSLKOpiq4n6rKIBystudent@serverb.lab.experiment
The key's random image is:
+----RSA 2048--------------------+
|                                |
|      o                          |
|    S                           |
|  .B + .                        |
| .0 . 0 =+ 0.0 |               |
| + = . + .X 0 .0 |             |
| Eoo 0. + +g=+ =|               |
+----[SHA256]--------------------+
```

## 2. On servera, configure the user student to accept logins authenticated by the SSH key pair you created for the user student on serverb. The student should be able to log in to server using SSH without entering a password.

### 2.1. Use the ssh-copy-id command to export the public key /home/student/.ssh/review3_key.pub from servera to serverb.

```
[student@serverb ~]$ ssh-copy-id -i .ssh/review3_key.pub student@servera
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: ".ssh/review3.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter
out any that are already installed
/usr/bin/ssh-copy-id: INFO: key(s) remain to be installed -- if you are prompted
now it is to install the new keys
student@servera's password: 1
```

Number of key(s) added: 1

Now try logging into the machine, with: ssh 'student@servera'
and to make sure that only the key(s) you wanted were added.

### 2.2. Use the ssh command to confirm that you can log in to serverb as using the SSH private key /home/student/.ssh/review3_key without being prompted for the password.

```
[student@serverb ~]$ ssh -i .ssh/review3_key student@servera
...output omitted...
[student@servera ~]$
```

### 2.3. Log out of server.

```
[student@servera ~]$ exit
logout
Connection to server closed.
[student@servera ~]$
```

## 3. On serverb, configure the sshd service to prevent users from logging in as root with SSH.

### 3.1. Set the parameter PermitRootLogin to no in the /etc/ssh/sshd_config. You may use the command sudo vim /etc/ssh/sshd_config to edit the configuration file.

### 3.2. Reload the sshd service.

```
[student@serverb ~]$ sudo systemctl reload sshd.service
```

## 4. On servera, configure the sshd service to prevent users from using their passwords to log in. Users should be able to authenticate using their private key of the SSH key pair.

### 4.1. Set the parameter PasswordAuthentication to no in the /etc/ssh/sshd_config. You may use the command sudo vim /etc/ssh/sshd_config to edit the configuration file.

### 4.2. Use the systemctl reload command to reload the sshd service.

```
[student@serverb ~]$ sudo systemctl reload sshd.service
```

## 5. Create a tar archive named /tmp/log.tar contains the contents of /var/log on serverb. Remotely transfer the tar archive to the directory /tmp/servera, authenticating using student /home/student/.ssh/review3_key as the student user's private key using the SSH key for authentication.

### 5.1. Use the sudo tar command to create another archive named /tmp/log.tar as the superuser containing the contents of /var/log.

```
[@serverb ~]$ sudo tar -cvf /tmp/log.tar /var/log
[sudo] password for student: student
...output omitted...
```

### 5.2. Use the scp command to remotely transfer the archive file /tmp/log.tar to the directory /tmp on servera. Specify /home/student/.ssh/review3_key as the private key of the SSH key pair.

```
[@serverb ~]$ scp -i .ssh/review3_key /tmp/log.tar servera:/tmp
log.tar 100% 14MB 57MB/s 00:00
```

## 6. Configure the rsyslog service on serverb to log all messages that receives the priority level of debug or higher to the /var/log/grading-debug. This configuration should be set in /etc/rsyslog.d/grading-debug.conf file which you should create.

### 6.1. Create the file /etc/rsyslog.d/grading-debug.conf with the following content. You may use sudo vim /etc/rsyslog.d/grading-debug.conf to create the file.

```
debug /var/log/grading-debug
```

### 6.2. Use the systemctl command to restart the rsyslog service.

```
[@serverb ~]$ sudo systemctl restart rsyslog
```

### 6.3. Use the logger command to generate log message having priority debug.

```
[@serverb ~]$ sudo logger -p debug Testing
```

### 6.4. Confirm that the log message Testing is saved in the /var/log/grading-debug file.

```
[@serverb ~]$ sudo tail /var/log/grading-debug
...Output omitted...
Mar 12 09:55:22 serverb student Testing
```

## 7. Use the yum command to install the zsh package, available in the BaseOS repository, on serverb.

```
[@serverb ~]$ sudo yum install zsh
...output omitted...
Is this ok [y/n]: y
```

## CHAPTER 7 Comprehensive Review

```
...output omitted...
Installed:
zsh-5.5.1.el18.x86_64

Complete!
```

## 8. Use the yum command to enable the default module stream for the module python36 and install all the packages from stream, on serverb.

```
[student@serverb ~]$ sudo yum install python36
...output omitted...
Is this ok [y/N]: y
...output omitted...
Installed:
python3-6.6.18.module+el18
pip3-9.8.3-13.el18.noarch

Complete!
```

## 9. Set the timezone of server to Asia/Kolkata.

### 9.1. Use the sudo timedatectl command to set the timezone of server to Asia/Kolkata.

```
[student@serverb ~]$ sudo timedatectl set-timezone Asia/Kolkata
```

### 9.2. Log out of server.

```
[student@serverb ~]$ exit
logout
Connection to serverb closed.
[student@workstation ~]
```

## Evaluation

On workstation, run the lab rhca-rh124-review grade command to confirm success of this exercise.

```
[student@workstation ~]$ lab rhca-rh124-review grade
```

## Finish

On workstation, run lab rhca-rh124-review finish to complete the comprehensive review. This script deletes the files and directories created during the start of the comprehensive review and ensures that the environment on serverb is clean.

```
[student@workstation ~]$ lab rhca-rh124-review finish
```

This concludes the comprehensive review.

# LAB MANAGING NETWORKS

In this review, you will configure and test network connectivity.

# OUTCOMES
You should be able to:

- Configure the network settings.
- Test network connectivity.
- Set a static host name for the system.
- Use locally resolvable canonical host names to connect to systems.

# BEFORE YOU BEGIN
Log in to workstation as student using student.

On workstation, run lab rhcesa-rh124-review4 start to start the comprehensive review. This script creates the necessary files to set up the environment correctly.

```
[student@workstation~$] lab rhcesa-rh124-review4 start
```

# INSTRUCTIONS
Accomplish the following tasks on server to execute the exercise.

- Determine the address of the Ethernet interface and its active connection profile on server.
- On server, create a new connection profile called static for the available Ethernet interface that statically sets network settings and does not use DHCP. It should be based on the settings in the following table.

| IPv4 address | 172.25.250.111 |
| Netmask | 255.255.255.0 |
| Gateway | 172.25.250.254 |
| DNS server | 172.25.250.254 |

Set the server's Ethernet interface to use the updated network settings displayed in the table above.

- Ensure that the host name of server is statically set to server-review4.lab.example.com.
- On server, set client-review4 as the canonical host name for the IPv4 address 172.25.250.10 of the servera.lab.example.com.
