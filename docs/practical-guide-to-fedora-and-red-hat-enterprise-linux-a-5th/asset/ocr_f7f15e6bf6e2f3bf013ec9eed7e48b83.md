name) of the Samba server. Windows then displays the directories that the Linux system is sharing. To view the shares on the Linux system named **bravo**, for example, you would enter \\bravo. From this window, you can view and browse the shares available on the Linux system. If you set a share so that it is not browsable, you need to enter the path of the share using the format \\servername\sharename.

# Mapping a Share

Another way to access a share on a Samba server is by mapping a share. Open **My Computer** or **Explorer** on the Windows system and click **Map Network Drive** from one of the drop-down menus on the menu bar (found on the **Tools** menu on Windows XP). Windows displays the **Map Network Drive** window. Select an unused Windows drive letter from the **Drive** combo box and enter the Windows path to the share you just created. (When you use *system-config-samba* to create a share, the share has the same name as the name of the directory you are sharing.) The format of the windows path is \\*hostname*\*sharename*. For example, to map */tmp* on *bravo* to Windows drive *J*, assuming the share is named *tmp* on the Linux system, select *J* in the **Drive** combo box, enter \\bravo\tmp in the **Folder** text box, and click **Finish**. You should be able to access the *tmp* directory from *bravo* as *J* (*tmp*) on the Windows machine. If you cannot map the drive, refer to “Troubleshooting” on page 768.

# Accessing Windows Shares from Linux

As a client, Samba enables you to view and work with files on a Windows system from a Linux system. This section discusses several ways of accessing Windows files from Linux.

# smbtree: Displays Windows Shares

The *smbtree* utility displays a hierarchical diagram of available shares. When you run *smbtree*, it prompts you for a password; do not enter a password if you want to browse shares that are visible to the *guest* user. The password allows you to view restricted shares, such as a user’s home directory in the [homes] share. Following is sample output from *smbtree*:

```
$ smbtree
Password:
MGS    \\PB
          \\PB\mark           pb Samba
          \\PB\MainPrinter   Home Directories
          \\PB\ADMIN$        MainPrinter
          \\PB\IPC$          IPC Service (pb Samba)
          \\PB\tmp           mgs temp
```