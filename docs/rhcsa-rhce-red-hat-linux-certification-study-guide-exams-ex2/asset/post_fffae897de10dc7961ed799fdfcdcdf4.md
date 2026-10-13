
## Samba as a Client

11. The command that can be used to mount remotely shared Microsoft directories is mount.cifs. The mount -t cifs command is also an acceptable answer.

## Samba Troubleshooting

12. The command that can test a Samba configuration file for errors is testparm.

## LAB ANSWERS

### Lab 1: Install and Start Samba

The chapter lab on Samba is designed to be easy to follow. However, you'll need explicit Linux knowledge to complete some specific steps. Answers to these steps can be found in the following:

- 1. You've installed the “CIFS file server” package group, which includes one RPM, samba.
- 2. One way to find all related Samba packages is with the yum search samba | grep samba command. You can then install noted packages with the yum install packagename command. Samba 4 packages are not supported for RHEL 6, at least not yet.
- 3. The Trusted Services section of the Firewall Configuration tool should make it easy to set up a local firewall to support communication to local Samba servers and clients.
- 4. You can use the chkconfig smb on command, the ntsysv tool, or the Service Configuration utility described in Chapter 7 to make sure Samba starts the next time you boot Linux.
- 5. Use the service smb start command to begin the Samba service. The /etc/init.d/smb start command is functionally equivalent.
- 6. One way to verify that Samba is running is to look for the existence of the smbd and nmbd processes in the process table. Use ps aux | grep mbd to see if these processes are present. Another way is with a service command such as service smb status command.

### Lab 2: Review Samba Documentation

This lab should familiarize you with the available documentation for the Samba File Server. When you run the man smb.conf command, it will open the manual for the main Samba configuration file.

You should be able to search through the file with vi-style commands. For example, to search for the hosts allow directive, going forward in the file, type in

```
/hosts allow
```

and press n to see the next instance of that directive. Alternatively, to search backward, type in the following:

```
?hosts allow
```

and press n to see the previous instance of that directive in the man page.

From the browser, you should be able to review Samba documentation. This lab directs you to sample stanzas for shared directories. Of course, you can browse around other Samba documentation. Learn what you need as a reference for the job, or for an exam.

### Lab 3: Configure Samba Global Settings

This lab assumes that you've backed up the smb.conf file from the /etc/samba directory.

- 1. To use SWAT, you'll first need to enable it with the associated Extended Internet Super Server. One way to do so is with the following commands:
  - # /etc/init.d/xinetd restart
  - # chkconfig swat on
- 2. Next, direct a browser to http://localhost:901. SWAT should prompt you for a username and password. By default, the root username and associated password will support access to SWAT.
- 3. Many administrators stick with the standard Microsoft Windows workgroup name of WORKGROUP. You can find it in the output from the smbclient -L //clientname command.
- 4. To limit access to a Samba server, you can do so in the Globals section, with the hosts allow directive. Of course, you can also do so by directly editing the smb.conf file in the /etc/samba directory.
- 5. To limit access from a specific computer, you can do so in the Globals section, with the hosts deny directive. Of course, you can also do so by directly editing the smb.conf file in the /etc/samba directory.
- 6. Make sure to click the Commit Changes button in SWAT. Then open a command line, and make Samba read the changes with the service smb reload command.
- 7. Before committing the changes, you can test them with the testparm command.

```
# /etc/init.d/xinetd restart
```

```
# chkconfig swat on
```

8. When testing the connection from another system, use the smbclient command. You'll need to allow access through UDP ports 137 and 138 for that purpose, something possible with the Trusted Services section of the Firewall Configuration tool.

9. If you need a fresh version of the smb.conf file, delete or move the existing version of the file from the /etc/samba directory and run the yum reinstall samba-common command.

### Lab 4: Configure a Share to a Home Directory

If successful, only one remote user will get access to his home directory via Samba, something that can be tested with appropriate smbclient and mount.cifs commands. One way to implement the requirements of this lab is with the following steps.

- 1. Open the main Samba configuration file, `/etc/samba/smb.conf`, in a text editor.
- 2. Navigate to the `[homes]` share in the last part of this file.
- 3. Unless there is already an appropriate limitation in the `[global]` section in this file, you can limit the `[homes]` share with the hosts allow = .example.com.
- 4. Add a guest ok = no to the `[homes]` stanza.
- 5. Add a valid users = username directive with the name of the desired user.
- 6. Commit the changes. Add the desired user to the Samba authentication database with the smbpasswd -a username command.
- 7. Restart or reload the Samba daemon, smb, under the Status menu or with the appropriate service command.
- 8. Save the changes made so far.
- 9. Test the result from a remote system with the smbclient command. You should also be able to use the mount.cifs command from a client root account, with the -o username=username switch, to mount the shared user home directory.

### Lab 5: Configure a Share to a Public Directory

This lab can be a continuation of Lab 4. You're just adding another stanza to the main Samba configuration file.

- 1. At the end of the file, start a `[public]` stanza. Add an appropriate comment for the stanza.
- 2. Set path = /home/public.
- 3. Make sure to set hosts allow = .example.com. Save your changes to the smb.conf file.

4. Set permissions for the public share with the following commands:

```
# mkdir /home/public
# chmod 1777 /home/public
```

Create a new directory, /home/public; configure that share and call it public. Set the hosts allow setting, and list the domain associated with your network. Deny access to all other systems.

The 777 setting for permissions grants read, write, and execute/search permissions to all users (root, root's group, and everyone else). The 1 at the beginning of the permission value sets the sticky bit. This bit, when set on directories, keeps users from deleting or renaming files they don't own.

5. Commit the changes to the currently running Samba service with the service smb reload command.

6. When testing the result from a remote system, any username in the local Samba database should work.

### Lab 6: Configure a Shared Network Directory, Limited to a Group

This lab may take a significant amount of work. You'll need to set up a group of users, with group ownership of a dedicated directory. Since that discussion in Chapter 8 was based on an RHCSA requirement, you'll have to repeat that process in this lab.

Once complete, you'll want to add the following directives to the stanza for the shared group directory:

```
create mask = 0770
directory mask = 2770
```

### Lab 7: Persistency Check

It's important to make sure that the configured service actually runs after a reboot. In fact, it's best to make sure the configured service works after a SELinux relabel, but that process can take several minutes or more. And it's quite possible that you won't have that kind of time during an exam.

1. To complete many Linux configuration changes, you need to make sure that the service will start automatically when you reboot your computer. In general, the key command is chkconfig. In this case, the chkconfig smb on command sets up the smbd daemon to become active when you boot Linux in a standard runlevel.

2. You can use various commands to perform an orderly shutdown, such as shutdown, halt, init 0, and more.
