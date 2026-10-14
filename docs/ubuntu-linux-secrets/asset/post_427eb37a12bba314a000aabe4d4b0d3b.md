
```
public = no
read only = yes
printable = yes
```

This section defines a printer share that only the userIDs frank, melanie, and nick can access from the network. Because the printable parameter is enabled, they don't need to have write permission to the /home/frank/spool directory for them to be able to print from the shared printer.

## Creating a Samba Server

Now that you've seen the different parts of the smb.conf configuration file, let's try to get a working server going on the network. There are three things you need to do to get your Samba server ready for the network:

- ♦ Edit the smb.conf configuration file.
- ♦ Add Samba user passwords to the system.
- ♦ Restart the Samba software.

The following sections walk through each of these processes.

## Editing the smb.conf File

You'll first need to configure your Samba server for your network. Follow these steps to start your server:

- 1. Open the smb.conf file in a text editor. If you're using the Ubuntu server installation from the console, you'll need to use a command-line editor such as vim. You can open the file using the vim editor using the command sudo vim /etc/samba/smb.conf
- 2. Set the workgroup to an existing workgroup or to a new workgroup. The workgroup line defines what Windows network workgroup to belong to: workgroup = WORKGROUP
- If you're using your Ubuntu server on an existing Windows network, entering the workgroup name here allows your server to appear in the Network Neighborhood browse list so that clients can connect to it without having to know its name.
- 3. Remove the comment from the interfaces line to enable connectivity from other network devices. The default setting should be interfaces 127.0.0.1/8 eth0
- Use the ifconfig command at the command line to ensure that the Ethernet port defined (eth0) is also active on your server.
- 4. Remove the comment from the security line to enable user-level security. This allows you to run your Samba server as a standalone server on the network and manage your own user accounts on the Ubuntu server.
- 5. Remove the comments from the [homes] section. There are three lines used in the [homes] section: [homes] comment = Home Directories browseable = no

If you want to allow users to browse to their home folder, change the browseable setting to yes.

- 6. Remove the comment from the read only line, and change the setting to no. This allows your users to write files to their home folder:
```
read only = no
```

- 7. Remove the comment from the valid users line. This setting restricts users to connecting only to their own home folder:
```
valid users = %S
```

- 8. Remove the comments from the printing and printcap name lines for the CUPS server entry. This enables your Samba server to share any printers defined in the CUPS server:
```
printing = cups
printcap name = cups
```

- 9. Save the new smb.conf file and exit the editor.

Now you have the Samba server configuration set for your network environment. The next step is to create the Samba account passwords for your users.

## Defining Samba Passwords

The default Samba configuration in Ubuntu uses the Ubuntu user account system to track users in the Samba configuration. However, there’s one problem with this setup. When a user attempts to connect to the Samba server with his or her userID, Windows servers and clients pass the password using an encryption scheme. Samba must know what the encrypted password is to be able to authenticate the user login request.

To do that, the Samba software maintains a separate password file that contains the user passwords encrypted by the Windows encryption algorithm. You must set the Samba user passwords separate from the Ubuntu passwords for this to work.

The tool used to encrypt Samba passwords is called smbpasswd. You must use the smbpasswd program to define each Ubuntu user account that’s going to access the Samba server. To define a user account password for the first time, you must use the -a parameter:

```
rich@testbox:~$ sudo smbpasswd -a test
New SMB password:
Retype new SMB password:
Added user test.
rich@testbox:~$
```

This creates a Samba password for the new user account. If you need to change the password for the account, you don’t need the -a parameter:

```
rich@testbox:~$ sudo smbpasswd test
New SMB password:
Retype new SMB password:
rich@testbox:~$
```

You’ll need to do this for all Ubuntu users who want to connect to their home folder as a Windows shared drive via the network.
