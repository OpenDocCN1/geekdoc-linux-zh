+   retrans=#—Sets the number of minor retransmission time-outs that occur before a major time-out. When a major time-out occurs, the process is either aborted (soft mount) or a "Server Not Responding" message appears on your console.

+   retry=#—Sets how many minutes to continue to retry failed mount requests, where # is replaced by the number of minutes to retry. The default is 10,000 minutes (which is about 1 week).

+   bg—If the first mount attempt times out, try all subsequent mounts in the background. This option is very valuable if you are mounting a slow or sporadically available NFS file system. By placing mount requests in the background, CentOS can continue to mount other file systems instead of waiting for the current one to complete.

![](bbox=[0.077, 0.337, 0.16, 0.363])

If a nested mount point is missing, a time-out to allow for the needed mount point to be added occurs. For example, if you mount /usr/trip and /usr/trip/extra as NFS file -ss:tems, if /usr/trip is not yet mounted when /usr/trip/extra tries to mount, /usr/trip/extra will time out. Hopefully, /usr/trip will come up and /usr/trip/extra will mount on the next retry.

+   fg—If the first mount attempt times out, try subsequent mounts in the foreground. This is the default behavior. Use this option if it is imperative that the mount be successful before continuing (e.g., if you were mounting/usr).

Any of the options that don't require a value can have no prepended to have the opposite effect. For example, nobg indicates that a mount should not be done in the background.

# Using autofs to Mount NFS File Systems on Demand

Recent improvements to autodetecting and mounting removable devices have meant that you can simply insert or plug in those devices to have them detected, mounted, and displayed. However, to make the process of detecting and mounting remote NFS file systems more automatic, you still need to use a facility such as autofs. If it is not installed, you can install the autofs package with the yum install autofs command.

With the autofs facility configured and turned on, you can cause any NFS shared directories to mount on demand. If you know the hostname and directory being shared by another host computer, you can simply change (cd) to the autofs mount directory (/net by default) and have the shared resource automatically mount and be accessible to you.

The following steps explain how to turn on the autofs facility:

+   As root user from a Terminal window, open the /etc/auto.master file and look for a line that appears as follows:

/net -hosts

This causes the /net directory to act as the mount point for the NFS shared directories you want to access on the network. (If there is a comment character at the beginning of that line, remove it.)