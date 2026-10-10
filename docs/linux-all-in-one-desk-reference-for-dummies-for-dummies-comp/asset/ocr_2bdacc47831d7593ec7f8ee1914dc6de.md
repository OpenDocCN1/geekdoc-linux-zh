As the example shows, the format of each line in `/etc/passwd` looks like this:
`username:password:UID:GID:GECOS:home dir:shell`

Table 2-1 explains the meaning of the seven fields in each `/etc/passwd` entry.

**Table 2-1** *Meaning of the Fields in /etc/passwd File*

| This Field | Contains |
| :--- | :--- |
| username | An alphanumeric username, usually eight characters long and unique (Linux allows usernames to be longer than eight characters, but some other operating systems do not.) |
| password | When present, a 13-character encrypted password. (An empty field means that no password is required to access the account. An x means the password is stored in the `/etc/shadow` file, which is more secure.) |
| UID | A unique number that serves as the user identifier. (`root` has a UID of 0 and usually the UIDs between 1 to 100 are reserved for nonhuman users such as servers; keeping the UID less than 32,767 is best.) |
| GID | The default group ID of the group to which the user belongs (`GID` 0 is for group `root`, other groups are defined in `/etc/group`, and users can be, and usually are, in more than one group at a time.) |
| GECOS | Optional personal information about the user. (`The finger` command uses this field and GECOS stands for General Electric Comprehensive Operating System, a long-forgotten operating system that’s immortalized by the name of this field in `/etc/passwd`.) |
| home dir | The name of the user’s home directory |
| shell | The command interpreter (shell), such as `bash` (`/bin/bash`), that executes when this user logs in |

# ## Managing Groups

A group is something to which users belong. A group has a name and an identification number (ID). After a group is defined, users can belong to one or more of these groups.

You can find all the existing groups listed in `/etc/group`. For example, here is the line that defines the group named `wheel`:
`wheel:x:10:root,naba`