
`user1@localhost` `$` `/home/user1`

## 7. `sudo -u <user>`

**Function:** Restricts permissions. Administrators can authorize ordinary users to perform root operations without knowing the root password. When switching via `su`, a password is required to execute `sudo`. The `sudo` command is only available to `root` by default. `sudo` permissions are specified by security policies, default located in `/etc/sudoers`. If other users need to use `sudo`, `/etc/sudoers` configuration can be modified via `visudo`, which is equivalent to `vim /etc/sudoers`.

```bash
[root@localhost]# visudo
```

`## Allow root to run any commands`

`root ALL=(ALL) ALL`

This means `root` can execute any command on any machine, where:
- `root`: represents the `root` user.
- `ALL`: represents any host.
- `(ALL)`: represents as any user.
- `ALL`: represents executing any command.

To allow `user` to execute all `root` commands, the command is:
(1) Modify `/etc/sudoers` to grant appropriate permissions to `user`.

```bash
[root@localhost]# visudo
```

`## Allow root to run any commands`

`root ALL=(ALL) ALL`

`user ALL=(ALL) ALL`

Save and exit. Enable password functionality.

## Deploying users and groups

Batch creating user instances:

(1) Create the user information file, command is:

```bash
[root@localhost]# vim userlist

[root@localhost]# cat userlist

auser1:x:1001:1001:/home/user1:/bin/bash

auser2:x:1002:1002:/home/user2:/bin/bash

auser3:x:1003:1003:/home/user3:/bin/bash

auser4:x:1004:1004:/home/user4:/bin/bash
```

(2) Create user passwords, command is:

```bash
[root@localhost]# vim passwordlist

[root@localhost]# cat passwordlist

auser1:123456

user2:123456

user3:123456

user4:123456
```

(3) Use `newusers` to add users in batch, command is:

```bash
[root@localhost]# newusers userlist
```

(4) Disable shadow passwords, command is:

```bash
[root@localhost]# pwconv
```

This command takes the shadow password from `/etc/shadow` and writes it back to `/etc/passwd`; this is for the next password operation, effectively disabling shadow functionality.

(5) Set passwords, command is:

```bash
[root@localhost]# chpasswd <passwordlist
```

(6) View user information file `/etc/passwd`, command is:

```bash
[root@localhost]# tail -1 /etc/passwd

auser1:x:1001:1001:/home/user1:/bin/bash

auser2:x:1002:1002:/home/user2:/bin/bash

auser3:x:1003:1003:/home/user3:/bin/bash

auser4:x:1004:1004:/home/user4:/bin/bash
```

(7) View `/etc/shadow`, command is:

```bash
[root@localhost]# tail -1 /etc/shadow

auser1:x:123456:99999:7:0:99

auser2:x:123456:99999:7:0:99

auser3:x:123456:99999:7:0:99

auser4:x:123456:99999:7:0:99
```

# Project 3: Deploying Users and Groups

- **Password**: Starts with the group, shows cannot use password, so there are no group administrators.
- **Administrator**: Accounts for group administrators.
- **Group User List**: Displays all users belonging to this group, multiple users separated by commas.

## 3.1.6 Group Management

### 1. `groupadd` or `addgroup`

**Syntax:** `groupadd [options] group`

**Function:** Creates a user group. This command can only be executed by the `root` user.

The options are as follows:

- `-g`: Used to specify the GID for creation. For example, to create a group with ID `1003` and view it:

```bash
[root@localhost ~]# groupadd -g 1003
```

```bash
[root@localhost ~]# tail -1 /etc/gshadow
```

When using `groupadd` to create a new group without specifying a GID, the system assigns one, starting from `1000`. The result is a line added to `/etc/group` and `/etc/gshadow` files containing the new group record.

### 2. `groupmod [options] group`

**Function:** Modifies attributes of a user group. This command can only be executed by the `root` user.

After a group is created, its attributes can be modified as needed, primarily including the group name and ID.

The options are as follows:

- `-g id`: Used to modify the group ID.
- `-n name`: Modifies the user group name.
- `-o`: Forces acceptance of a duplicate group GID. For example, to rename the group `"group"` to `"group1"` with GID `1002`:
