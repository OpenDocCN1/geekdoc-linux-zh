even or actual Microsoft Windows servers. smclient is a flexible program and can be used to browse other servers, send and retrieve files from them, or print to them. As you can imagine, this is also a great debugging tool, since you can quickly and easily check whether a new Samba installation works correctly without having to find a Windows client to test it.

In this section, we'll show you how to do basic browsing, remote file access, and remote printer access with smclient. Remember that smclient is a flexible program, limited only by your imagination.

> NOTE smclient program is packaged separately in Ubuntu. You'll have to install it explicitly by running a command, like:
m@ubuntu-server:-$ sudo apt-get -y smclient

# Browsing a Server

With many graphical interfaces around, we've come to equate browsing with "point-and-click." When your intention is simply to find out what a server has to offer, it's not enough of reason in itself to support an entire GUI.

Using smclient with the -L option allows you to view the offerings of a Windows file server or Samba server without having to use a GUI. Here's the format of the command:

```
smclient -L hostname
```

Here, hostname is the name of the server. For example, if we want to see what the local host (the Samba server running locally) has to offer, we type

```
smclient -L localhost
```

You will be prompted for a password, but you can press ENTER to complete the command.
To list the shares on the Samba server again without being prompted for a password, you can use the -U (or -N) option. This implies that you want to be authenticated as the guest user, which has no password. You type the following:

```
[server]# smclient -U -L localhost
Domain=[MYGROUP] OS=[ Windows ] Server=[Samba 4.*]
Sharename Type       Comment
-------------------------------------------------------
samba-share Disk      This folder contains shared documents
IPC IPC               IPC Service (Samba Server Version 4*)
Domain=[MYGROUP] OS=[ Windows ] Server=[Samba 4.*]
....<OUTPUT TRUNCATED>....
```

Notice the presence of the share we created earlier in line 4 of the preceding output.