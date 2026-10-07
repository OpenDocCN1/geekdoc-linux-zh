# v4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

If you can use this technique to go through your /etc/rc.d/ directory to turn off services that you do not need. Since I'm not running an all laptop, and don't need PCMCIA services nor do I have wireless network support on my workstation, I'll make sure they do not discard accordingly.

```
root@forensic1:~ chmod 644 /etc/rc.d/rc.pcmcia
root@forensic1:~# chmod 644 /etc/rc.d/rc.wireless
```

You might also consider doing the same with other services:

```
root@forensic1:~# chmod 644 /etc/rc.d/rc.gpm-sample
```

If want to know what each script does, or if you are unsure of the purpose of a service started by a particular rc script, just open the script with your paging program (less, for instance) and read the comments. Turning off a service you need is just as leaving an unneeded service running. Learn what each script starts, and when, and enable it discard accordingly.

For example, here's the comments at the beginning of /etc/rc.d/rc.yp:

```
root@forensic1:~# less /etc/rc.d/rc.yp
#!/bin/sh
# /etc/rc.d/rc.yp
#n# Start NIS (Network Information Service). NIS provides network-wide
# distribution of hostname, username, and other information databases.
# After configuring NIS, you will need to uncomment the parts of this
# script that you want to run.
# NOTE: for detailed information about setting up NIS, see the
# documentation in /usr/doc/yp-tools, /usr/doc/ypbind
# /usr/doc/psyserv, and /usr/doc/Linux-HOWTOs/NIS-HOWTO.
<continues>
```

I would suggest using ssh running (via the /etc/rc.d/rc.ssh script). If you do not think you will use SSH, as you become more proficient with Linux, you will find that
ssh, the "secure shell", becomes an important part of your toolbox.