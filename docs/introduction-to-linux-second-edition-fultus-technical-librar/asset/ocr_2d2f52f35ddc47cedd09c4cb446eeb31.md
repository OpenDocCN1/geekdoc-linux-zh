| Command | Meaning |
| :------- | :------- |
| directory | moving files from this directory. |
| chmod 600 file | A private file only changeable by the user who entered this command. |
| chmod 644 file | A publicly readable file that can only be changed by the issuing user. |
| chmod 660 file | Users belonging to your group can change this files, others don't have any access to it at all. |
| chmod 700 file | Protects a file against any access from other users, while the issuing user still has full access. |
| chmod 755 directory | For files that should be readable and executable by others, but only changeable by the issuing user. |
| chmod 775 file | Standard file sharing mode for a group. |
| chmod 777 file | Everybody can do everything to this file. |

Table 3.9. File protection with chmod

If you enter a number with less than three digits as an argument to **chmod**, omitted characters are replaced with zeros starting from the left. There is actually a fourth digit on Linux systems, that precedes the first three and sets special access modes. Everything about these and many more are located in the Info pages.

# 3.4.2.2 Logging on to another group

When you type **id** on the command line, you get a list of all the groups that you can possibly belong to, preceded by your user name and ID and the group name and ID that you are currently connected with. However, on many Linux systems you can only be actively logged in to one group at the time. By default, this active or *primary group* is the one that you get assigned from the `/etc/passwd` file. The fourth field of this file holds users' primary group ID, which is looked up in the `/etc/group` file. An example:

```
```
asim:~> id
uid=501(asim) gid=501(asim) groups=100(users),501(asim),3400(web)

asim:~> grep asim /etc/passwd
asim:x:501:501:Asim El Baraka:/home/asim:/bin/bash

asim:~> grep 501 /etc/group
asim:x:501:
```
```