# Inspecting Footprints

# 17.2.2

daemons856 Linux services that are spawned at boot time to perform specific operations without any need for user interaction. Linux servers are often configured to host numerous daemons, SSH, web servers, and databases, to mention a few.

System administrators often rely on custom daemons to execute ad-hoc tasks and sometimes neglect security best practices.

As part of our enumeration efforts, we should inspect the behavior of running processes to hunt for any anomaly that might lead to an elevation of privileges.

Unlike Windows systems, on Linux we can list information about higher-privilege processes as the ones running inside the root user context.

We can enumerate all the running processes with the ps command and since it only takes a single snapshot of the active processes, we can refresh it via the watch command. In the following example, we will run the ps command every second via the watch utility and grep the results on any occurrence of the word 'pass'.

```
joe@privvesc:~$ watch -n 1 "ps -aux | grep pass"
joe 16687 0.0 0.1 6352 2996 S+ 05:41 0:00 -n 1 ps -aux |
groot 16880 0.0 0.0 2384 756 ? S 05:41 00:00 sh -c sshpass -p
'Lab123' sh -t e127.0.0.1 'sleep 5;1'
root 16681 0.0 0.0 2356 1640 S 05:41 0:00 sshpass -p zzzzz s sshpass
-t e127.0.0.1 sleep 5;exit
```

> Listing 488 - Harvesting Active Processes for Credentials

In Listing 488, we notice the administrator has configured a system daemon that is connecting to the local system with eve's credentials in clear text. Most importantly, the fact that the process is running as root does not prevent us from inspecting its activity.

Another holistic approach we should take into consideration when enumerating for privilege escalation is to verify whether we have rights to capture network traffic.

tcpdump is the facto command line standard for packet capture, and it requires administrative access since it operates on raw sockets. However, it is uncommon to find IT personnel accounts have been given exclusive access to this tool for troubleshooting purposes.

To illustrate the concept, we can run tcpdump as the joe user who has been granted specific permissions to run it.

```
tcpdump cannot be run without sudo permissions. That is because it needs to set up raw sockets85 in order to capture traffic, which is a privileged operation.
```