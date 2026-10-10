# Setting Up a File Server

# 17

This shows that the Samba server is running on the local computer. Shared directories and printers, as well as servers in the workgroup, appear here. If the Samba server is not running, you will see “Connection refused” messages. You need to start the Samba service as described in the “Starting the Samba Service” section earlier in this chapter.

# Firewall Open?

If the Samba server is running, it should begin broadcasting its availability on your LAN. If you try to access the server from a Windows or Linux client on your LAN but get a “Connection refused” error, the problem may be that the firewall on your Linux Samba server is denying access to the NetBIOS service. If you have a secure LAN, you can type the following (as root user) to flush your firewall rules temporarily.

```
# iptables -F
```

Then, try to connect to the Samba Server from a Windows or Linux client. If you find that you can connect to the server, turn the firewall back on:

```
# service iptables restart
```

You then need to open access to ports 137, 138, 139, and 445 in your firewall so that the Samba server will be able to accept connections for services. (See Chapter 13 for information on modifying your firewalls.)

# User Passwords Working?

Try accessing a shared Samba directory as a particular user (from the local host or other Linux system on your LAN). You can use the smbclient command to do this. Here’s an example:

```
# smbclient //localhost/home/timothy/files -U timothy
added interface ip=10.0.0.1 bcast=10.0.0.255 nmask=255.255.255.0
Password: ******
Domain=[WORKG1] OS=[Unix] Server=[Samba 3.2.4]
smb: \\
```

In this example, smbclient connects to the directory share named tmp as the Samba user named timothy. If the password is accepted, you should see information about the server and a smb:\> prompt. If you cannot access the same shared directory from a Windows client, it’s quite possible that the client is passing an improper username and password.

> TIP The smbclient command, used here to list server information and test passwords, can also be used to browse the shared directory and copy files after you are connected. After you see the smb:\> prompt, type help to see the available commands. The interface is similar to any FTP client, such as SFTP.