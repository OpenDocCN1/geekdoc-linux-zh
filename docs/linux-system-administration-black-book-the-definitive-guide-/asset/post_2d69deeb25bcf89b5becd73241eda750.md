
25. If you want to only offer read-only access to this share, then change **read only** to **yes**. However, this defeats the whole purpose of having a public upload space.
26. If you want only authenticated users to have access to this space, then change **public** to **no**.
27. Proceed to:

```conf
[public]
	comment = Public Stuff
	path = /home/samba
	public = yes
	writable = yes
	printable = no
	write list = @staff
```

28. If you want to utilize this definition to allow the public to view information on a share, but want to allow only particular users and/or groups to write to it, then uncomment it so that it looks like the following:

```conf
[public]
	comment = Public Stuff
	path = /home/samba
	public = yes
	writable = yes
	printable = no
	write list = @staff
```

29. If you want to rename this share, then change the name within the brackets.
30. If you want to change the identifier to be more descriptive, such as **Staff Policy Documents**, then change the value assigned to the **comment** option.
31. If you want to keep these documents in a different place, then change the **path** statement.
32. If you want no one to have write permissions through Samba mounting the export, then change the **writable** value to **no**. The **printable** option is actually unnecessary here, because you are not defining a print share.
33. Change the **write list** value to consist of a list of users and groups— in `@group` format—who are allowed to write to this share through SMB if you leave **writable** set to **yes**.
34. See the following section to build a share definition from scratch.

## Building A File Share Statement

To build a file share statement from scratch, do the following:

1. If you have not already done so, log in as root to the machine whose partitions you want to offer.
2. If you are not already editing the file, type "vi /etc/smb.conf" to open the Samba configuration file.
3. Type "G" to go to the end of the file.
4. Type "o" to open a new line at the end of the file and then enter Insert mode.
5. Start with the share name. This name is formatted as follows: **[sharename]**. The name should have no spaces or punctuation. You can use any term except the reserved shares: [global], [homes], and [printers].
6. Typically, the first option you set after the share name is **comment**. Indent this line under the share name so that it is obvious at a glance where this share definition starts and ends. The comment should be descriptive, but without giving too much information away to potential intruders. For example, so far, you might have the following:

```
[ProjectP]
comment = Documents needed by ProjectP staff
```

7. Next is often the **path** option. Here, you set the file system location of files that you want to share. Try to isolate this directory as much as possible so that people will not get access to files they should not be able to see or touch. For example, the definition might now be similar to the following:

```
[ProjectP]
comment = Documents needed by ProjectP staff
path = /Projects/P/
```

8. This point is where a "typical" share definition stops being consistent. From here on, most shares are different from one another, so you can be a bit more freeform. A list of options you might want to utilize is given in Table 18.6. Examine this list thoroughly.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_570_0.png)

Table 18.6 Popular options used in individual Samba share definitions.

| Option | Purpose | Value(s) | Example |
| :--- | :--- | :--- | :--- |
| **admin users** | Sets a list of users who access this share with superuser-like privileges. Strong security implications arise when you utilize this option, because not only do you allow the defined users to have the power to empty the share, change permissions, and more, but if an intruder gains access using one of these accounts, that intruder can alter the files as they see fit. | A space-separated list of users | **admin users = joe barb** |
| **browseable** | Specifies whether to allow Samba clients to see this share when requesting a list of shares available. | **yes** or **no** | **browseable = yes** |
| **case sensitive** | Specifies whether Samba handles file names as case-sensitive or ignores case entirely. | **yes** or **no** | **case sensitive = no** |
| **copy** | Tells Samba to copy all parameters from another share, and override those that are duplicated in this share. | Share name with no brackets | **copy = ProjectB** |
| **default case** | Sets the default case for file names created by clients. | **upper** or **lower** | **default case = lower** |
| **dont descend** | Explicitly refuses to allow Samba clients to access particular subdirectories. | A comma-separated list of subdirectories | **dont descend = /Projects/ProjectB/needs_approval** |
| **follow symlinks** | Tells Samba whether to follow symbolic links out of the share. | **yes** or **no** | **follow symlinks = no** |
| **force group** | Sets all users accessing this share to belong to the listed group. | Group name, or **+group** if you want only users who are already assigned to this group to create files under the group's name | **force group = project_staff** |
| **force user** | Sets all users accessing this share to this particular username after the client properly authenticates. | Username | **force user = staff** |
| **guest account** | Sets the user account to use for guest logins. | Name of account; typically, this should be an account without normal shell access | **guest account = smbguest** |
| **guest ok** | Allows unauthenticated logins, and assigns all clients without a valid login to the guest account. | **yes** or **no** | **guest ok = yes** |
| **guest only** | Specifies that if **guest ok** is set to **yes**, all clients accessing this share will be logged on through the guest account. | **yes** or **no** | **guest only = yes** |
| **hide files** | Sets particular files to be accessible, but not show up in a file listing. | A slash-separated listing of files, with the wildcards `*` and `?` available, and also the substitution variables listed in Table 18.3 | **hide files = master_data/master*/temp?*** |
| **hosts allow** | Provides access control that enables you to fine-tune who is allowed to mount this share. If a host is explicitly allowed, then it will not be denied even if listed in **hosts deny**. | Comma-, space-, or tab-separated list of host identifiers, as specified in the coverage of /etc/hosts.allow in Chapter 9 | **hosts allow = .colors.org** |
| **hosts deny** | Provides access control that enables you to fine-tune who is allowed to mount this share. | Comma-, space-, or tab-separated list of host identifiers, as specified in the coverage of /etc/hosts.deny in Chapter 9 | **hosts deny = ALL** |
| **invalid users** | Specifies users who cannot log in to this share. | **Usernames; @group** for both NIS netgroups and standard user groups, **+group** for standard user groups, and **&group** for NIS netgroups | **invalid users = root, wheel, @admin** |
| **locking** | Enables locks to be placed on files that a client has open for editing. | **yes** or **no** | **locking = yes** |
| **mangle case** | Sets whether to change file names that do not match the **default case**. | **yes** or **no** | **mangle case = no** |
| **mangled map** | Slightly alters file names requested and placed by SMB clients. | The item to change, with the asterisk wildcard allowed; the format is **(one other)** | **mangled map = (*.html *.htm)** |
| **mangled names** | Sets whether to convert non-DOS-formatted file names to DOS format. | **yes** or **no** | **mangled names = no** |
| **max connections** | Sets the maximum number of clients that can connect to this service. | Number of clients, or 0 for infinite | **max connections = 5** |
| **oplocks** | Enables use of opportunistic file locks to ensure that a file cannot be altered while someone else is altering it. | **True** or **False** | **oplocks = True** |
| **postexec** | Sets a command or script to run on the server when a client disconnects from this service. | Path to command, with standard substitutions listed in Table 18.3 | **postexec = /root/bin/leave.scr** |
| **preexec** | Sets a command or script to run on the server when a client connects to this service. | Path to command, with standard substitutions listed in Table 18.3 | **preexec = /bin/fortune** |

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_572_0.png)
