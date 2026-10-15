
# LISTING 7.11 Entry in syslog.conf to Monitor Logins

```
...
auth.info			/var/log/authlog
...
```

The file /var/log/authlog (and you are free to choose any suitable name) will, depending on the number of logins per day, grow very fast. You need to make sure to rotate the file periodically and store the copies in a secure location if they are needed in a later investigation. After adding this entry into the configuration file, you need to tell syslog to re-read its configuration by sending the process the hang-up signal. You need to create the file if it does not exist and try to test the functionality by using a non-working login, as shown in Listing 7.12.

# LISTING 7.12 Restarting syslog and a Non-Working Login

```
root@unixhost> ps -ef | grep [Ss]syslogd
root      350   1  0 14:56:05 ?        0:00 /usr/sbin/syslogd
root@unixhost> kill -HUP 350
root@unixhost> exit
erikk@unixhost> su - knapf
Password:
su: Sorry
erikk@unixhost> su -
Password:
Commodore 64 38512 Bytes Ready!
# tail -2 /var/log/authlog
Sep  1 11:46:03 unixhost su: [ID 810491 auth.crit] 'su knapf' failed
for erikk on /dev/pts/2
Sep  1 11:46:16 unixhost su: [ID 366847 auth.notice] 'su root'
succeeded
for erikk on /dev/pts/2
```

Listing 7.12 demonstrates a failed login by user erikk while switching to the user knapf. If you would search for the string failed in the log file, then you would be presented with all failed logins that occurred since the last rotation of the log file, provided that log file was not tampered with, another reason to monitor such files. The greeting string on the system was chosen deliberately; it is of no concern to anyone what operating system is used on a machine. The fact that the system administrators know is sufficient.

## 7.3.3 When and How to Use chkrootkit

If you should suspect that something is wrong with a system and you further suspect a break-in, then it is time to analyze the system thoroughly. One program to be used in that respect is called chkrootkit.

A rootkit is a set of programs that were installed on the system, enabling an intruder to work as root on that system without your knowing. A rootkit manipulates settings and programs on the system in a way that prevents detecting the break-in or makes it at least very difficult to find any traces of it. Because you cannot be sure what was modified or replaced, you need to use untainted binaries to detect such a set of programs (see Section 5.1.4, "Copy the Important Commands"). If you need to learn about the inner workings of rootkits and how to detect them, you should consult the information on http://www.chkrootkit.org. Using a rootkit on another system could be a punishable offense in most parts of the world.

To make one thing perfectly clear first: not every system showing some kind of strange behavior was taken over by a cracker. You need to check first if the system displays uncommon patterns of network activity. You need another system, known to be clean, to run these checks. If you were not able to find another reason for the strange behavior and still suspect an occupied system, then you need to check the machine.

The first step you need to take is to check the system using aide (see Section 7.2.3, "Checking Files with aide") or using the lists created in Section 7.2.2, "A Simple File Checker." If there is any reason to believe that something is wrong with the system, then it should be taken off the network immediately. This does not mean that you should shut down the system, but rather disconnect it from the network at once. After that, you need to check the system for the reported modified files, configurations, etc. Which commands, settings, and programs were modified? These modifications allow you to assess the scope of the break-in. If you should not have experience regarding the treatment of a compromised machine, get professional help. If the incident damaged the company's data or the system itself, then reporting that damage is governed by strict rules. These rules include a defined procedure concerning how the compromised system is to be secured. Doing computer forensics requires extensive training. If any proof should get lost in the process, insurance and law enforcement cannot do anything for you. Describing the detailed steps required is beyond the scope of this book. If you know the required steps, proceed.

The executable program chkrootkit and the required system commands usable on the compromised system should be on a CD-R. You have to mount that CD-R and start the program as shown in Listing 7.13.
