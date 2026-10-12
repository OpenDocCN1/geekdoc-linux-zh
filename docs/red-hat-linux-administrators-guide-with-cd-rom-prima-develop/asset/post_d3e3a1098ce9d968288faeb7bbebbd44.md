
crypt() function. Once a password has been hashed with MDS, you can no longer convert it back to a simple text file. This helps to prevent spying eyes from gaining easier access to the original file, but does not eliminate the possibility that the password could still be guessed using brute force cracking methods.

## NOTE

Shadow passwords originally began on such UNIX-based systems as Solaris, but they have since been adopted by nearly all Linux distributions, including Red Hat. On the latest Red Hat release you have the option to install shadow passwords and enable MDS hashing. These are selected by default and it is a wise decision to allow them to remain so.

Unique system users such as nobody and bin do not normally allow a password to be affixed to them. To ensure that these types of files are not misused, it is a good idea to verify that no password is kept in the field that normally stores the encrypted passwords. An asterisk, or star, should appear instead of the password. This ensures that no one can physically log in under that assumed username. The same can be done on a regular user. By replacing the gibberish of encrypted text with an asterisk, you ensure that the user is no longer validated to log on with a password.

Listing 5.1 shows sample output from an /etc/shadow file. Notice the difference between the users with UIDs under 500 and the five valid users—four normal users and root.

### Listing 5.1 A Selection Taken from a Sample /etc/shadow File

```
root:*$1$sYQciqsIZUxHm3xc3IRpMgUWr4YJmL E0:10873:0:99999::7:-1:134538460
bin::10819::99999::7::
daemon::10819::99999::7::
adm::10819::99999::7::
ip::10819::99999::7::
sync:10819::99999::7::
shutdown::10819::99999::7::
halt:*10819::99999::7::
mail::10819::99999::7::
news::10819::99999::7::
uucp::10819::99999::7::
operator:*:10819:0:99999:7:::
games:*:10819:0:99999:7:::
gopher:*:10819:0:99999:7:::
ftp:*:10819:0:99999:7:::
nobody:*:10819:0:99999:7:::
xfs:!!:10819:0:99999:7:::
gdm:!!:10819:0:99999:7:::
kerry:$1$rpUfM.763$meGe$A8MW7/.NiVIWZ9H4q/:10873:0:99999:7:-1:-1:134538460
karen:$1$0Dhio04/$q..XcvVqw9rjIWwGydL/N1:10821:0:99999:7:-1:11261:134537332
calvin:$1$XAF$JDUD3SXJ/QwmIu67j7yvn36jtTTF/:10873:0:99999:7:-1:-1:134538436
andrew:$1$h32NmuQZBsR22NEMi6sFeXithd7d:/:10873:0:99999:7:-1:-1:134538436
```

The regular logins have a string of nonessential characters and numbers, whereas the system users possess an asterisk in their password field.

## Pseudoroot Management via sudo

Like all great superpowers, root also has its Achilles’ heel. Root’s drawbacks lie in its overwhelming power. When you become superuser, there are technically no logs kept other than those for the bash_history or the respective shell history as implemented by that root user. This means that once any actions are committed, they can just as easily be erased from the any shell history files. Since root is also a GID (group ID), anyone who compromises the group file can still gain access to root owned files. Because its power is so overwhelming, root can wipe out all the users and gain control of the box for whoever becomes root. As is often stated in Linux newsgroups, “God, root, what’s the difference?” On a Linux machine, this is very much the case. The only way to combat someone gaining root access or corrupting your files is to reformat and start over or to restore from a clean backup. These also are not great solutions.

The ability to perform maintenance on Linux is crucial. One person cannot do everything that needs to be done, especially if the system has a large contingent of users. But tasks such as adding new users, performing backups, and changing passwords all require root access. If you do grant root access to another user for performing maintenance tasks, make certain you trust that person implicitly and that he or she will not do anything prejudicial to your system. Sharing the responsibility of root carries with it the burden of taking blame should anything be corrupted due to negligence or carelessness.

In response to the problem of sharing root-owned tasks, the UNIX community developed **sudo**. By using the program *sudo* (or *superuser*), a system administrator can enable certain users (or groups of users) to run some (or all) commands as root while also logging all commands and arguments. This feature takes care of the logging issue as posed by the regular superuser. The *sudo* program operates on a per-command basis and is not a replacement for the shell. In other words, only certain root-owned commands can be delegated to other users. The root password need not be shared with multiple users. Nor when executing *sudo* commands does the user gain a root-owned shell or have any more root-like power, except for that which has been allotted him or her.

The *sudo* program operates by checking a configuration file called */etc/sudoers*. A list of users and commands defines who can perform what command with root permissions. This file is created by root and can be edited only by root. The users listed can carry out only those functions to which this file gives them access.

## Configuring the sudo Program

You can find the *sudo* program in several locations on the Internet. The default location is <http://www.courtesan.com/sudo/>, yet a simple Internet query will turn up several mirror sites. After downloading and installing *sudo* properly on the system, you need to configure the */etc/sudoers* file and determine who will have permission to perform what action. You can edit this file by hand, but it is recommended that you use the special binary, *visudo*, that comes installed with the package. The *visudo* command brings up a text editor; *vi* is the default editor, hence the binary program's name. This text editor enables you to modify the settings while constructing a database file in a format understood by *sudo*.

Listing 5.2 shows a potential */etc/sudoers* file.

### Listing 5.2 An Example /etc/sudoers File

```
# Host alias specification
Host_Alias    LAN=quasi,sequitur,nihilo
Host_Alias    WAN=k2,lopenap,olympus,granite,nebo

# User alias specification
User_Alias    IT=kerry,brad,john,dan
User_Alias    SALES=bill,greg,dave
User_Alias    BOSS=mark
User_Alias    OFFICE=rox,andrea

# Command alias specification
Cmd_Alias     DUMP=/usr/sbin/tcpdump,/sbin/rdump
Cmd_Alias     BACKUP=/usr/sbin/ufsbakeup
Cmd_Alias     SHELL=/bin/sh,/bin/csh,/bin/tcsh,/bin/ksh
Cmd_Alias     SU=/bin/su
Cmd_Alias     MISC=/bin/rm,/bin/cat
Cmd_Alias     SHUTDOWN=/usr/sbin/shutdown
Cmd_Alias     USERS=/usr/scripts/adu,/usr/scripts/diu

# User specification
IT            ALL=ALL
kerry         WAN=ALL, LAN=quasi,sequitur
brad          WAN=ALL, LAN=nihilo
john          WAN=SHUTDOWN, /usr/scripts/adu
rox           quasi=/usr/bin/shutdown -[hr] now,MISC
andrea        lonepeak=USERS
mark          WAN=SHELLS
dave          nebo=BACKUP, granite=DUMP
greg          LAN=SHELLS

# End of file
```

## Clarifying sudo Options

This section describes the several categories of options configured in Listing 5.2.

### Host Alias Specifications

There are only two categories here, LAN and WAN. LAN defines the Linux boxes currently located within her internal network. They are running Red Hat and Solaris respectively. WAN specifies the servers that handle all accounts and perform different functions such as DNS, mail, news, Web, and virtual Web accounts. They are all running Red Hat.

There are four user aliases: IT, SALES, OFFICE, and BOSS. IT includes all technical staff, SALES consists of the sales staff who need access to limited items, OFFICE handles all the billing requirements and needs only to add and delete users, and BOSS, or the user mark, should only be using different shells. Even though BOSS has only one entry, other entries are foreseeable. For this reason, you temporarily give BOSS only one entry, but optimize the user mark in the “User specification” category.

### Command Alias Specifications

Command aliases are lists of commands with or without associated command-line arguments. The entries in Listing 5.2 should be self-explanatory.

### User Specifications

The users listed in Listing 5.2 are as follows:

| User | Description |
|---|---|
| *IT* | All staff included under the IT User Aliases specification may run any of the commands as defined by the Host Aliases specifications. |
| *kerry* | This user may run all commands on the WAN, but may run commands on only two or three of the machines listed in the LAN category. |
| *brad* | Likewise, the user brad may run all commands on machines listed in the WAN portion of Host specifications, but may only run commands on nihilo, one of the machines in the LAN category. |
| *john* | On all the machines in the WAN category, the user john may run the shut-down command and may only run the adu script. The adu script is a simple script that adds users to Solaris machines, while the adu script deletes users. |
| *rox* | The user rox may run only the shutdown command on one machine, quasi, and also the two additional commands listed under the MISC section. |
| *Andrea* | This user may only run system maintenance commands as defined by the USERS category and only on one machine, lonepeak. |
| *mark* | I want to limit this user’s access to the system as much as possible. However, because he is management, he does require some access to important files. He may run only those commands listed under the SHELLS category and only on WAN machines. |
