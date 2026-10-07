
# v.4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

by changing the permissions. If an rc script is executable, it will run. If it is not executable then it is passed over. As an example, let's have a look at the OpenSSH (secure shell) portion of rc.inet2:

```
root@forensic:~# cat /etc/rc.d/rc.inet2
...
# Start the OpenSSH SSH daemon:
if [ -x /etc/rc.d/rc.sshd ]; then
echo "Starting OpenSSH SSH daemon: /usr/sbin/sshd"
/etc/rc.d/rc.sshd start
fi
...
```

Again, this position of rc.inet2 checks to see if rc.sshd is executable. If it is, then it runs the command /etc/rc.d/rc.sshd start. Note that the rc services can have either start, stop or restart passed as arguments in most cases. So, in this particular example:

- /inittab calls /etc/rc.d/rc.M
- /etc/rc.d/rc.M calls /etc/rc.d/rc.inet2 (if rc.inet2 is executable)
- /etc/rc.d/rc.inet2 passes the command /etc/rc.d/rc.sshd start (if rc.sshd is executable).

Earlier we discussed file permissions. Now let us look at a practical example of changing permissions for the purpose of stopping select services from starting at boot time. A look at the permissions of /etc/rc.d/rc.sshd shows that it is executable, and so will start when rc.inet2 runs:

```
root@forensic:~# ls -l /etc/rc.d/rc.sshd
-rw-xr-x- 1 root 1726 Mar 10 2016 /etc/rc.d/rc.sshd*
```

To change the permissions to prevent the SSH service from starting at boot time, I execute the following:

```
root@forensic:~# chmod 644 /etc/rc.d/rc.sshd
root@forensic:~# ls -l /etc/rc.d/rc.sshd
-rw-r--r-- 1 root 1726 Mar 10 2016 /etc/rc.d/rc.sshd
```

The directory listing shows that I have changed the executable status of the script, and therefore prevented the service from starting when the system boots. Depending on your color terminal settings, you may also see the color of the file change.

If you can use this technique to go through your /etc/rc.d/ directory to turn off services that you do not need. Since I'm not running a laptop, and don't need PCMCIA services nor do I have wireless network support on my workstation, I'll make sure they do not start accordingly.

```
root@forensic1:~# chmod 644 /etc/rc.d/rc.pcmcia
root@forensic1:~# chmod 644 /etc/rc.d/rc.wireless
```

You might also consider doing the same with other services:

```
root@forensic1:~# chmod 644 /etc/rc.d/rc.gpm-sample
```

If you want to know what each script does, or if you are unsure of the purpose of a service started by a particular rc script, just open the script with your paging program (less, for instance) and read the comments. Turning off a service you need is just as leaving an unneeded service running. Learn what each script starts, and when, and enable it start accordingly.

For example, here's the comments at the beginning of /etc/rc.d/rc.yp:

```
root@forensic1:~# less /etc/rc.d/rc.yp
#!/bin/sh
# /etc/rc.d/rc.yp
# Start NIS (Network Information Service). NIS provides network-wide
# distribution of hostname, username, and other information databases.
# After configuring NIS, you will need to uncomment the parts of this
# script that you want to run.
# NOTE: for detailed information about setting up NIS, see
# documentation in /usr/doc/yp-tools, /usr/doc/ypbind
# /usr/doc/yperv, and /usr/doc/NIS-HOWTO.
```

I would suggest using ssh running (via the /etc/rc.d/rc.ssh script). If you do not think you will use SSH, as you become proficient with Linux, you will find that the "secure shell" becomes an important part of your toolbox.

## Host Based Access Control

We continue our baseline security discussion with host based access control. Note that this is NOT a firewall. This is access control at the host level. In simple terms, we can determine who can access our system by two files, /etc/hosts.deny and /etc/hosts.allow. For this we use TCP wrappers.

Basically, TCP wrappers work like this: When a server configured to run through TCP wrappers receives a connection request, the inetd daemon calls the "wrapper" service /usr/sbin/tcpd. The tcpd program checks /etc/hosts.allow file to see if the connection is permitted, and runs the requested service accordingly.

If I want to see only those lines that are not commented, I can do this:

```
root@forensics:~# cat /etc/inetd.conf | grep -v ^
time      stream tcp wait root internal
time      dgram wait   root internal
comsat    dgram wait   /usr/sbin/tcpd in.comsat
auth      stream wait   /usr/sbin/in.ident in.ident
```

The command shown shows the contents of /etc/inetd.conf and pipes the output to grep. We will use grep to display lines that DO NOT start with #. The character "^" means "start of line". Running the above command gives me only those lines that are actually used in the configuration. In order to understand how these services work and to find specific information on what is running on our system, let's have a more detailed look at the line in our output:

```
comsat    dgram wait   root       /usr/sbin/tcpd in.comsat
```

Since this line is not commented out, we know that the service is allowed to run on our system. Let's find out what it does and how to disable it, and confirm that it's disabled. The services that left running on a basic install are generally left for a reason. I would not recommend commenting out any of these lines without understanding the consequences. For educational purposes, at the end of the lesson, we'll likely keep it enabled. The purpose of this exercise is how you can trace running services, and find out what they do. If you are running Linux (any flavor), and you do not know what services are running and why, then you need to rethink your approach to securing your forensic workstation.

So what does the comsat service do? We can simply run the man command on the server program that is called. In this case, the program is in.comsat. If we run man in.comsat, we see that this service is used to notify a user of incoming mail (biff).

Now we're going to do a little deeper and learn about some other Linux commands and files as we disable and enable the service. Pay attention to all of these commands on your workstation, regardless of the distribution. Knowing what is "normal" for your particular setup allows you to recognize when things have changed, either through malicious intent or by accident.

The following commands, with everything else in this guide, are best learned by hands on experimentation – keeping in mind that if you are not using wrappers, your output is likely to differ, especially if TCP wrappers is not used in whatever distribution you happen to be running.

First we explore the network port being used by the service, and see if it is running. We know the service is called comsat. We can use the /etc/services file to determine the port number to service mapping name.

```
root@forensici:~# cat /etc/services | grep comsat
biff    512/udp      #used by mail system to notify users
```

So, using the grep command to find the line containing comsat we find that it is using UDP port 512. To determine if 512 is open, we can use the netstat command:

```
root@forensici:~# netstat -anu
Active connections (servers and established)
Proto Recv-Q Send Local Address           State
udp 0               0.0.0.0:512             0.0.0:*
udp 0               0.0.0.0:37              0.0.0:*
udp 0               0.0.0.0:68              0.0.0:*
```
