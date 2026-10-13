7. You may retain the remaining lines; where the fi ends the if loop, the done ends the do loop, and the exit 0 returns a success message:

```
fi
done
exit0
```

8. Save the changes. Execute the script from the local directory. Since the script name is testscript, the following command executes its contents from the local directory:

```
$ ./testscript
```

9. Check the contents of the docfiles file. If the script worked, you'll find existing .doc files in that directory.

# CERTIFICATION OBJECTIVE 12.02

# Kernel Run-Time Parameters

Kernel run-time parameters, as defined in the RHCE objectives, relate to files in the /proc/sys directory and the sysctl command. Closely related is the /etc/sysctl.conf configuration file, as that's used by the sysctl command during the boot process to add parameters to various files in the /proc/sys directory. So it's appropriate to start this section with a look at that sysctl.conf file.

# How sysctl Works with /etc/sysctl.conf

The /etc/sysctl.conf file was briefly discussed in Chapter 1, as it controls IPv4 forwarding. To review, you can enable IPv4 forwarding in two steps. First, change the following boolean directive to activate IPv4 forwarding in the configuration:

```
net.ipv4.ip_forward = 1
```

Then make the system re-read the configuration file with the following command:

```
# sysctl -p
```