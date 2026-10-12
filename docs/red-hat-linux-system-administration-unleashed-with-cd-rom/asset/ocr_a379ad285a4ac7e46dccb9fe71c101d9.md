Now that we have covered /proc, the next section will look at some simple ways to alter files in /proc.

# Using echo to Alter System Behavior

Previously we examined /proc and what it is, and introduced the concept of changing system values within /proc to alter how the system operates. What we have not done is examine exactly how this can be accomplished with relative ease. We will look at two examples of passing information to the system using terminal echoing.

> **Note**
> 
> All of the examples discussed may or may not work depending on the revision of the kernel. For example, some parameter locations may be different or they may not even exist.

> **Note**
> 
> These examples are taken directly from http://www.linux.com/tuneup/database.phtml?Kernel/ and http://www.nl.linux.org/linuxxperf/.

# Understanding the Anti-Ping Setting

The first example is the anti-ping setting. For the sake of an example, let's say that on your corporate intranet, someone keeps pinging the Linux server Larry to see if it is alive instead of just browsing to the Web server. Although you would like to tell the user how you appreciate his ingenuity, you would prefer he just browsed to Larry's server and you will let him know if there are any problems. Of course, he doesn't listen. As a matter of fact, he has taken to running ping for hours on end. As a temporary measure, you would like to shut off the inbound ping requests without altering any other protocols. There is a long way to do this, which we will not get into, but the easiest way is to simply try this:

```
$ echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all
```

This will cause the system to ignore all ping requests.