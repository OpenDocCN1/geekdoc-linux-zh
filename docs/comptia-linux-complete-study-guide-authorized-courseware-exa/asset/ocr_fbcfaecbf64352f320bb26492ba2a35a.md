# ## Disabling Unused Servers

Quite a few server programs ship with most Linux distributions, which can be a great advantage—you don't need to hunt for servers you want to run. On the other hand, this very advantage can be a drawback—if you're not careful, you can end up running a server and not even realize it's installed! For this reason, you should periodically search for servers and shut down any that you find that aren't really necessary. You must begin this task by locating unwanted servers. Several tools to do so exist, such as `netstat`, `lsof`, and remote network scanners. You can also search your local configuration files for clues about what may be running. Disabling unused servers can be done by uninstalling the package or by reconfiguring the server.

# ## Using netstat

One way to begin diagnosing network security is to look for network activity or open ports on a computer. One tool that can help in this respect is **netstat**. This program is the Swiss Army knife of network status tools; it provides many different options and output formats to deliver information about routing tables, interface statistics, and so on. For spotting unnecessary servers, you can use netstat with its `-a` and `-p` options, as shown here:

```
```
# netstat -ap
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address                 Foreign Address               State
PID/Program name
tcp        0      0 *:ftp                 *:*                   LISTEN
690/inetd
tcp        0      0 teela.rodsbooks.com:ssh nessus.rodsbooks.com:39361 ESTABLISHED
787/sshd
```
```

![](bbox=[0.15, 0.63, 0.26, 0.69])

I've trimmed most of the entries from this output to make it manageable as an example. Also, `netstat` can be run as an ordinary user, but it may not return as much information. Specifically, only root and a process's owner see the PID and program name of a process.

This version of the `netstat` command shows active network connections, which can reveal the presence of servers that are running on your computer. The Local Address and Foreign Address columns specify the local and remote addresses, including both the host-name or IP address and the port number or associated name from `/etc/services`. The first of the two entries shown here isn't actively connected, so the local address, the foreign address, and the port number are all listed as asterisks (*). This entry does specify the local port, though: *ftp*. This line indicates that a server is running on the ftp port (TCP port 21). The State column specifies that the server is listening for a connection. The final column in this output, under the PID/Program name heading, indicates that the process with a process