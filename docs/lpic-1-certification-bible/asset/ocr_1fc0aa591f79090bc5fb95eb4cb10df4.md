# ## Telnet

The Telnet service and application allows remote access to a machine. Using Telnet, you can access the shell on a remote system. Telnet requires the user to log in with a valid user name and password, as though they were logging on to the machine locally. All of the user’s configuration files are used, and the user has access to all of the files and programs that can normally be accessed through the shell. By default the root or superuser account cannot log in via Telnet. If a user needs to access the system as root via Telnet, he or she must first log in using a standard login ID and then use the `su` command to access the root account. This procedure is done because the user name and password sent to the remote computer aren’t secure. As with FTP, the Telnet program could allow unauthorized users to access the system if they locate a valid user name and password. For this reason, use caution when allowing remote users to Telnet to a machine. Another, more secure alternative is SSH, which provides a more secure remote shell. The following is an example of the output produced by the Telnet utility:

```
```
# telnet deedee.the-nashes.net
Trying 10.254.90.135...
Connected to 10.254.90.135.
Escape character is '^]'.

Red Hat Linux release 6.2 (Zoot)
Kernel 2.2.14-5.0 on an i686
login:
```
```

# ## host

The `host` utility is used to look up hostnames on domain name servers. Information such as IP address, hostname, and mail servers can be discovered using this command. The following are examples of output produced by the `host` command:

```
```
# host www.the-nashes.net
www.the-nashes.net has address 216.254.90.131

# host 216.254.90.131
131.90.254.216.IN-ADDR.ARPA domain name pointer brain.the-nashes.net

# host the-nashes.net
the-nashes.net has address 10.254.90.131
the-nashes.net has address 216.254.90.131
the-nashes.net mail is handled (pri=10) by mail.the-nashes.net
```
```

The `host` command is covered in more detail in Chapter 16.

# ## ping

The `ping` utility is used to verify TCP/IP connectivity. This utility uses the ICMP protocol to send small packets of data to the specified host. The host then sends a response packet back to the local host. This is a useful utility for verifying network