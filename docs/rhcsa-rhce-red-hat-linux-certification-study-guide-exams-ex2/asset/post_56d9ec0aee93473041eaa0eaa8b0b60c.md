
Host- and user-based security on a Samba system can be enhanced with the following directives: invalid users, valid users, hosts allow, and hosts deny.

To repeat, this section is focused only on those directives relevant to the RHCE objectives.

## Share Settings

To see what SWAT can do to the share settings in the smb.conf configuration file, click Shares from atop the SWAT web-based menu. Click the drop-down text box associated with Choose Share, and then click Homes. Next to Change View To, click Advanced to reveal the screen shown in Figure 15-3. Relevant options fall into several categories.

### FIGURE 15-3 SWAT share settings

![](img/9139201cfcaf4292284a0eed074928e5_851_0.png)

Options on this page are straightforward. To create a second share, enter a name in the Create Share text box, and then click the Create Share button. You can then configure it in the text boxes that follow. When the process is complete, click Commit Changes. Many of the directives that appear were already explained in the global settings section but apply only to the local share. Those directives are not repeated here.

- **comment** Information included with the share name.
- **path** The path to the directory to be shared.
- **username** Substitute usernames where machine usernames are not available; rarely used.
- **force user** A user account assigned to all who connect to the share.
- **force group** A group account assigned to all who connect to the share.
- **read only** Shares so labeled can only be read.
- **guest only** Only guest user connections are allowed.
- **guest ok** Guest user connections are allowed; no password is required.

You'll note that most of these directives aren't covered here and in fact are rarely used.

## Server Status

To see the current status of Samba on the system, click Server Status from atop the SWAT web-based menu. As shown in Figure 15-4, it supports control of the Samba, NetBIOS, and Winbind daemons. If there are active connections, active shared directories, and files in use, they're also listed in this view.

## View Configuration

Any changes made with SWAT, once saved are written to the /etc/samba/smb.conf file. Click View. It includes a current read-only view of that file.

## User Management

You can manage the Samba user authentication database with SWAT. To do so, click Password from atop the SWAT web-based menu. As shown in Figure 15-5, it supports password changes for current users. In addition, you can use the screen shown to add new users to the local Samba authentication database.

### FIGURE 15-4 Default installed Apache home page

![](img/9139201cfcaf4292284a0eed074928e5_853_0.png)

But these are just front ends to the smbpasswd command. In either case, the user has to exist in the Linux authentication database. For example, the following command takes the current user michael and prompts for a new password:

```
# smbpasswd michael
```

Alternatively, the following command adds user donna to the Samba authentication database, prompting for a password:

```
# smbpasswd -a donna
```

The -d, -e, and -x options can respectively disable, enable, and delete the given user from the Samba authentication database.

## Test Changes to /etc/samba/smb.conf

After making any changes to /etc/samba/smb.conf, you should always test the system before putting it into production. A simple syntax check on the Samba configuration file is possible with the testparm utility, as shown in Figure 15-6. This does not actually check to determine whether the service is running or functioning correctly; it checks only basic text syntax and command stanzas.

### FIGURE 15-5 SWAT server password management

![](img/9139201cfcaf4292284a0eed074928e5_854_0.png)

The directives that are displayed are share stanzas, along with associated directives. For example, the [homes] share is not read only and is not browsable to all clients.

## Review User- and Host-Based Samba Security

As suggested in the RHCE objectives, you need to know how to configure "host-based and user-based security for" each service, including Samba. So while this section is repetitive, it's important.

To review, user-based security can be configured within the main Samba configuration file, smb.conf. Users specified in that file are configured in a separate database, normally in the /var/lib/samba directory, managed with the smbpasswd command.

### FIGURE 15-6

Review the Samba configuration with testparm

```
[root@Maui ~]# testparm
Load smb config files from /etc/samba/smb.conf
rlimit_max: rlimit_max (1024) below minimum Windows limit (16384)
Processing section "[global]"
Processing section "[printers]"
Loaded services file OK.
Server role: ROLE_STANDALONE
Press enter to see a dump of your service definitions

[global]
workgroup = MYGROUP
server string = Samba Server Version %v
log file = /var/log/samba/log.%m
max log size = 50
wins server = 127.0.0.1
cups options = raw

[homes]
comment = Home Directories
read only = No
browseable = No

[printers]
comment = All Printers
path = /var/spool/samba
printable = Yes
browseable = No
[root@Maui ~]#
```

User-based security is enabled for the system with the following option:

```
security = user
```

Users can be specified as allowed or denied with the invalid users and valid users directives. Those directives can be applied generally in the Global Settings section or applied per share in the stanza where the shared directory is configured.

Host-based security can be configured in both the Samba configuration file and any associated iptables-based firewalls. Hosts can be allowed or denied with directives such as hosts allow and hosts deny. In some configurations, you'll see synonyms for those directives, such as allow hosts and deny hosts.

For example, the following hosts allow directive can limit access to the specified network(s):

```
hosts allow = 127. 192.168.122. 192.168.100.
```

The 127. is not required; localhost addresses are always allowed unless specifically included in a hosts deny directive.

## Review Basic Samba Shares

Specifically for Samba, the RHCE objectives specify that you need to "provide network shares to specific clients" and to "provide network shares suitable for group collaboration."

To provide network shares to one or more specific clients, you'll need to include directives like valid users and invalid users in the stanza associated with a shared Samba directory.

To provide network shares suitable for group collaboration, you'll need to remember the following tasks:

- Set up an appropriate group and permissions on the directory to be shared.
- Configure the shared directory and files with the SELinux samba_share_t file type.
- Define a separate share stanza in the Samba configuration file, with appropriate values for writable, create mask, directory mask, and write list.

## EXERCISE 15-2

### Configuring Samba with Shares

In this exercise, you'll configure Samba to share a directory. For this purpose, you'll directly edit the /etc/samba/smb.conf file.

- 1. Create a /home/ftp/public directory. Change ownership to the ftp user and group, with full permissions for both (770).
- 2. Make sure to set appropriate SELinux settings for the directory with the following command:
  In addition, to make sure the changes survive a relabel of SELinux, you'll want to set up the file_contexts.local file in the /etc/selinux/targeted/contexts/files directory with a command such as the following:
- 3. Open the /etc/samba/smb.conf file in a text editor.

```
# chcon -R -t samba_share_t /home/ftp
```

```
# semanage fcontext -a -t samba_share_t /home/ftp
```

- 4. Configure Samba to share as public, in read-only mode, the /home/ftp/pub directory tree. In the Share Definitions section, you could add the following commands:
- 5. Allow guest access to all public shares. In smb.conf, this means adding the following line to the [pub] stanza:
- 6. To create a guest account, you'll need to add the following command in smb.conf:
- 7. Create a guest account for pcguest, associate it with an unused UID and GID 600. (If you already have a user with this ID, substitute an unused ID number.) Set the password as "anonymous." While you can do this with the Red Hat User Manager discussed in Chapter 8, the quickest way to do this is with the following commands:
- 8. Create separate log files for each computer host that connects. This is already active by default with the following command:
- 9. Write and save changes to the smb.conf file.
- 10. You can see if Samba is already running with the service smb status command. If it's stopped, you can start it with the service smb start command. If it's running, you can make Samba reread your configuration file with the following command:
  This final option allows you to change your Samba configuration without disconnecting users from the Samba server.

```
[pub]
    comment = shared FTP directory
    path = /home/ftp/pub
```

```
guest ok = yes
```

```
; guest account = pcguest
```

```
# useradd pcguest -u 600
# passwd pcguest
```

```
log file = /var/log/samba/%m.log
```

```
# service smb reload
```
