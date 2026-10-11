
This would look like this:

```
mount dellbert:/home /mnt/client1
```

- To have your system mount remote file systems automatically, you can edit the `/etc/fstab` and place an entry there to have it be mounted during the system's startup (when the system runs a `mount -a`):

```
dellbert:/home /mnt/data   nfs    rw    0    0
```

![](img/49f4f38f3aec011238fa50f89e643db3_504_0.png)

> Be aware of /etc/fstab entries that are invalid or mount commands that include host/share as the device. If you're not careful, you might think that a valid NFS share is a wrong answer or distractor.

## Samba

Samba is a 32-bit suite of programs that enable a Linux machine to function as a Windows-compatible file and print server and a Windows NT 4.0 domain controller.

![](img/49f4f38f3aec011238fa50f89e643db3_504_1.png)

> The exam objectives on Samba are very sparse. We'll stick to the objectives and put some tidbits in to help you out.

The Samba package consists of client and server components, with the server-side function provided by

- smbd—SMB/CIFS server, file, and printer sharing
- nmbd—Name resolution and browsing name proxy services

You need to know specifically that **nmbd** provides all the name resolution, browsing, and WINS support that Windows clients on a Linux network could need. When any of that is needed, that functionality is provided by the **nmbd** daemon.

The **smbd** daemon provides all the file and printer sharing functionality for the Windows clients on a Linux network. Although Linux clients can use Samba tools to access Windows resources via SMB/CIFS, and even each other via the same protocols, the majority of clients are Windows machines with Samba running on the Linux server to provide common resources to those clients.

### Samba's Configuration File

The Samba daemons are configured with the file `/etc/samba/smb.conf`. This file used to reside in the `/etc` directory but, like many others, has been moved in the last couple of years to its own directory structure.

> **ALERT**  
> If you see questions about the `smb.conf` file on the exam, it might appear as `/etc/smb.conf` or `/etc/samba/smb.conf`, but never as a choice between the two in the same question.

This file consists of three sections, all of which are important:

- **Global**—For options that affect the server environment and defaults for shares that don't have specific options.
- **Homes**—Thought to be for user home directory shares, Homes auto-provisions and creates user home directory shares for valid users.
- **Printers**—Not needed in later Samba versions because all printers are loaded automatically, it's now used for specific printer options or printer security.

The `smb.conf` file has more than 300 options.

> **TIP**  
> You can edit the `smb.conf` file directly or use a tool called Samba Web Admin Tool (SWAT). Take great care using SWAT, though, because it removes any customized configuration you might have added!

Entries in the `smb.conf` file typically take the following form:

```
keyword = value
```

Take great care when editing the file, and be sure to run the `testparm` command to check the syntax of your newly configured `smb.conf` file for errors.

### Important smb.conf Entries

The following section covers the basics and includes anything reputed to be on the exams, with a few extra items to help you.

Important *smb.conf* entries include

- workgroup—The value takes the form of a NetBIOS workgroup or domain name, with the same restrictions.
- server string—The value is a description only, such as I'm really a Linux box!
- hosts allow—The value is a host glob or IP range that effectively restricts the use of Samba services to those hosts.
- guest account—This provides a mapping to an account with functionality equivalent to the Windows guest account.
- security—The values here can be share, user, server, and domain, depending on the level of security you need.
- password server—This points all queries for authentication to a Windows domain controller by name, IP, or an asterisk (*) that uses a broadcast for the nearest domain controller.
- interfaces—The value here should be the IPs of the local interfaces you want Samba to listen and work with. Delete or remove this entry to service all interfaces.
- local master—With a value of yes, this causes the Samba server to participate vigorously in the local master browser elections.
- domain master—If set to yes, this causes Samba to also participate in the elections for the domain master browser, sometimes beating out any and all Windows domain controllers!
- domain controller—The value should be the local domain controller name or IP, used when the Samba server is a domain member.
- wins support—Either yes or no. If it’s yes, the Samba server performs WINS (Windows Internet Name Server, a poor man’s DNS) and accepts NetBIOS Name + IP registrations, queries for name resolution, and releases of the mappings.
- wins server—The value is the IP of the WINS server the Samba server is configured to query, and it should not point to the Samba server itself.

![](img/49f4f38f3aec011238fa50f89e643db3_506_0.png)

> Take great care to test your configuration with the **testparm** command because it prints the sections and their shares and displays a list of the options that are current for the Samba server.

### Setting Up a Simple Samba Server

To show how easy Samba is to configure, the next section is a quick setup of Samba to share a single directory for a user, including setting up the user for access. Follow these steps:

1. Edit the /smb.conf file and add the following share to the end of the file:

   ```
   # A share usable only the user snuffy
   [snuffydir]
       comment = a private share for snuffy
       path = /usr/share/snuffy
       valid users = snuffy
       public = no
       writable = yes
       printable = no
   ```

![](img/49f4f38f3aec011238fa50f89e643db3_507_0.png)

The comment is just that—the path is a valid path that **snuffy** has access to, the valid users are **snuffy**, the **public** keyword keeps other users out of that directory, the **writable** keyword allows **snuffy** to change the files therein, and **printable** being set to no means that no print job will be accepted into the directory.

2. Save and exit the file.
3. Run testparm to check the file.
4. Start Samba with /etc/rc.d/init.d/smb start (on Red Hat).
5. Confirm the service's start.
6. Add the user snuffy with the following command:

   ```
   useradd -m snuffy
   ```

7. Set the password for snuffy with the following command:

   ```
   passwd snuffy
   ```

   (Enter the password twice.)

8. Add the existing user to the Samba password files with the command shown here:

   ```
   smbadduser snuffy:snuffy
   ```

   (Enter the password twice.)

![](img/49f4f38f3aec011238fa50f89e643db3_507_1.png)

The first instance of the name **snuffy** represents the Linux user **snuffy**; the second **snuffy** after the colon represents the Samba user or the connecting Windows client user.

9. Go to a Windows client, map a share to the \\server\snuffydir share, and be sure to supply snuffy’s username and password when prompted.
10. Access the share.

## Monitoring SMB Connections

After you’ve connected to the share, copy an MP3 file or media file to the server. Then double-click it to run or listen to the file.

When the file is playing, run the **smbstatus** command to see what the user is doing. I often use this tool to see what’s going on with the server and to see what users are listening to:

```
smbstatus
```

This returns output similar to

```
Samba version 3.0.2a-Debian

PID  Username   Group       Machine
1268 rbrunson   users       wideboyxp (192.168.33.1)

Service     pid machine       Connected at
rbrunson    1268 your-fulkll0hzg Sun May 23 21:36:26 2004
Locked files:
Pid DenyMode Access     R/W           Name
1268 DENY_NONE 0x20089  RDONLY       LEVEL_II
/home/rbrunson/Ghost Of Freedom.mp3 Sun May 23 21:36:33
```

**smbstatus** shows statistics and file locks for whichever users are accessing via Samba on your server.

## Samba Client Connections

The vast majority of access using Samba is from Windows clients to Samba servers (typically running Linux or Unix), not the other way around.

For the odd instance when you need to determine that a server is advertising itself properly or to grab a file from a Samba server or Windows server and put it on a Linux client, you can use the **smbclient** command.

**smbclient** provides an FTP-like interface when run interactively, and it can run in command-line mode, such as the following command:

```
smbclient -L localhost
```

(Press Enter when prompted for a password.)
