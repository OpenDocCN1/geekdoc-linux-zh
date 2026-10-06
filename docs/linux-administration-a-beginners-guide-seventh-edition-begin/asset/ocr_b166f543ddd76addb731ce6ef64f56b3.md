# APPENDIX B Demo Virtual Machine 801

> TIP We cobbled together a little script that can be used for restoring the Demo VM to an almost clean or precustomization state. Running the script will remove most of the software packages, source code, history of commands, users/groups, configuration files, and other customizations that were done during the initial operating system installation.

```
# wget -c -O clean-up.sh http://linuxserverexperts.com/7e/
append-b/clean-up.sh
```

After downloading, and making sure that you can clean up (restore) the Demo VM server,

```
# chmod 755 clean-up.sh
./clean-up.sh
```

# Just Use It!

Out of the box and with the exception of the DHCP service, your Demo VM should be running virtually every service/daemon and that we've covered in this thick book. And to take the 'Just use it!' approach, you will need to at least know a little about the many components, services, or daemons that you want to use. In order to use it, you will need to know how to connect to the Demo VM via its IP address. The previous sections talked about the various ways to obtain this information.

Say, for example, you want to test the DNS server component that we discussed in Chapter 16 inside the Demo VM. IP address of the Demo VM is 192.168.1.202, you can use the dig command on your workstation or on the host system to query the DNS server running in the Demo VM by running

```
[client-$] dig @192.168.1.202 example.org MX
```

```
[client-$] smbclient -U -L 172.16.1.202
```

Suppose you want to list the Shares that we configured in Chapter 24 and the IP address of the Demo VM (Samba server) is 172.16.1.202. You can use the smbclient command on your workstation or on the host system to query the Samba server by running

As a final test of the immense magical capabilities of the Demo VM that we lovingly put together for you, let's query it for some fortune telling and what it says. The IP address of the Demo VM is 10.0.0.202, use the telnet program from computer to connect to port 17 on the Demo VM by running

```
you@anywhere ~$ telnet 10.0.0.202 17
Trying 10.0.0.202...
Connected to 10.0.0.202.
Escape character is '^'
<OUTPUT TRUNCATED>...
```