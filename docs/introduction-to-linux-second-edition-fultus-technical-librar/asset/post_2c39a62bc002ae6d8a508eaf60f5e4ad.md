
normal files. They may end in a .desktop or .lnk suffix; an example can be found in ~/.gnome-desktop:

```
[dupont@boulut .gnome-desktop]$ cat La Maison Dupont
[Desktop Entry]
Encoding=Legacy-Mixed
Name=La Maison Dupont
Type=X-Nutilus-home
X-Nutilus-Icon=temp-home
URL=file:///home/dupont
```

This example is from a KDE desktop:

```
[lena@venus Desktop]$ cat camera
[Desktop Entry]
Dev=/dev/sda1
FSType=auto
Icon=memory
MountPoint=/mnt/camera
Type=FSType
X-KDE-Dynamic-Device=true
```

Creating this kind of link is easy enough using the features of your graphical environment. Should you need help, your system documentation should be your first resort.

In the next section, we will study the creation of UNIX-style symbolic links using the command line.

### 3.3.5.2 Creating symbolic links

The symbolic link is particularly interesting for beginning users: they are fairly obvious to see and you don't need to worry about partitions.

The command to make links is `ln`. In order to create symlinks, you need to use the `-s` option:

```
ln -s targetfile linkname
```

In the example below, user freddy creates a link in a subdirectory of his home directory to a directory on another part of the system:

```
freddy:~/music> ln -s /opt/mp3/Queen/ Queen

freddy:~/music> ls -l
lrwxrwxrwx 1 freddy freddy 17 Jan 22 11:07 Queen -> /opt/mp3/Queen
```

Symbolic links are always very small files, while hard links have the same size as the original file.

The application of symbolic links is widespread. They are often used to save disk space, to make a copy of a file in order to satisfy installation requirements of a new program that expects the file to be in another location, they are used to fix scripts that suddenly have to run in a new environment and can generally save a lot of work. A system admin may decide to move the home directories of the users to a new location, disk2 for instance, but if he wants everything to work like before, like an /etc/passwd file, with a minimum of effort he will create a symlink from /home to the new location /disk2/home.

## 3.4 File security

### 3.4.1 Access rights: Linux's first line of defense

The Linux security model is based on the one used on UNIX systems, and is as rigid as the UNIX security model (and sometimes even more), which is already quite robust. On a Linux system, every file is owned by a user and a group user. There is also a third category of users, those that are not the user owner and don't belong to the group owning the file. For each category of users, read, write and execute permissions can be granted or denied.

We already used the *long* option to list files using the `ls -l` command, though for other reasons. This command also displays file permissions for these three user categories; they are indicated by the nine characters that follow the first character, which is the file type indicator at the beginning of the file properties list. As seen in the examples below, the first three characters in this series of nine display access rights for the actual user that owns the file. The next three are for the group owner of the file, the last three for other users. The permissions are always in the same order: read, write, execute for the user, the group and the others. Some examples:

```
marise:~> ls -l To_Do
-rw-rw-r-- 1 marise users     5 Jan 15 12:39 To_Do
marise:~> ls -l /bin/ls
-rwxr-xr-x 1 root   root    45948 Aug  9 15:01 /bin/ls*
```

The first file is a regular file (first dash). Users with user name *marise* or users belonging to the group *users* can read and write (change/move/delete) the file, but they can't execute it (second and third dash). All other users are only allowed to read this file, but they can't write or execute it (fourth and fifth dash).

The second example is an executable file, the difference: everybody can run this program, but you need to be *root* to change it.

The Info pages explain how the `ls` command handles display of access rights in detail, see the section *What information is listed*.

For easy use with commands, both access rights or modes and user groups have a code. See the tables below.

| Code | Meaning |
| :--- | :--- |
| 0 or - | The access right that is supposed to be on this place is not granted. |
| 4 or r | read access is granted to the user category defined in this place |
| 2 or w | write permission is granted to the user category defined in this place |
| 1 or x | execute permission is granted to the user category defined in this place |

Table 3.7. Access mode codes

| Code | Meaning |
| :--- | :--- |
| u | user permissions |
| g | group permissions |
| o | permissions for others |

Table 3.8. User group codes

This straight forward scheme is applied very strictly, which allows a high level of security even without network security. Among other functions, the security scheme takes care of user access to programs, it can serve files on a need-to-know basis and protect sensitive data such as home directories and system configuration files.

You should know what your user name is. If you don’t, it can be displayed using the id command, which also displays the default group you belong to and eventually other groups of which you are a member:

```
tilly:-> id
uid=504(tilly) gid=504(tilly) groups=504(tilly), 100(users), 2051(org)
```

Your user name is also stored in the environment variable USER:

```
tilly:-> echo $USER
tilly
```

### 3.4.2 The tools

#### 3.4.2.1 The chmod command

A normal consequence of applying strict file permissions, and sometimes a nuisance, is that access rights will need to be changed for all kinds of reasons. We use the chmod command to do this, and eventually to chmod has become an almost acceptable English verb, meaning the changing of the access mode of a file. The **chmod** command can be used with alphanumeric or numeric options, whatever you like best.

The example below uses alphanumeric options in order to solve a problem that commonly occurs with new users:

```
asim:~> ./hello
bash: ./hello: bad interpreter: Permission denied

asim:~> cat hello
#!/bin/bash
echo "Hello, World"

asim:~> ls -l hello
-rw-rw-r-- 1 asim asim 32 Jan 15 16:29 hello

asim:~> chmod u+x hello

asim:~> ./hello
Hello, World

asim:~> ls -l hello
-rwxw-r--- 1 asim asim 32 Jan 15 16:29 hello*
```

The + and - operators are used to grant or deny a given right to a given group. Combinations separated by commas are allowed. The Info and man pages contain useful examples. Here's another one, which makes the file from the previous example a private file to user *asim*:

```
asim:~> chmod u+rxw,go-rwx hello

asim:~> ls -l hello
-rwx----- 1 asim asim 32 Jan 15 16:29 hello*
```

The kind of problem resulting in an error message saying that permission is denied somewhere is usually a problem with access rights in most cases. Also, comments like, “It worked yesterday,” and “When I run this as root it works,” are most likely caused by the wrong file permissions.

When using **chmod** with numeric arguments, the values for each granted access right have to be counted together per group. Thus we get a 3-digit number, which is the symbolic value for the settings **chmod** has to make. The following table lists the most common combinations:

| Command | Meaning |
| :--- | :--- |
| chmod 400 file | To protect a file against accidental overwriting. |
| chmod 500 | To protect yourself from accidentally removing, renaming, or moving files from this directory. |
| chmod 600 file | A private file only changeable by the user who entered this command. |
| chmod 644 file | A publicly readable file that can only be changed by the issuing user. |
| chmod 660 file | Users belonging to your group can change this files, others don't have any access to it at all. |
| chmod 700 file | Protects a file against any access from other users, while the issuing user still has full access. |
| chmod 755 directory | For files that should be readable and executable by others, but only changeable by the issuing user. |
| chmod 775 file | Standard file sharing mode for a group. |
| chmod 777 file | Everybody can do everything to this file. |

Table 3.9. File protection with chmod

If you enter a number with less than three digits as an argument to **chmod**, omitted characters are replaced with zeros starting from the left. There is actually a fourth digit on Linux systems, that precedes the first three and sets special access modes. Everything about these and many more are located in the Info pages.

#### 3.4.2.2 Logging on to another group

When you type **id** on the command line, you get a list of all the groups that you can possibly belong to, preceded by your user name and ID and the group name and ID that you are currently connected with. However, on many Linux systems you can only be actively logged in to one group at the time. By default, this active or *primary group* is the one that you get assigned from the `/etc/passwd` file. The fourth field of this file holds users' primary group ID, which is looked up in the `/etc/group` file. An example:

```
asim:~> id
uid=501(asim) gid=501(asim) groups=100(users),501(asim),3400(web)

asim:~> grep asim /etc/passwd
asim:x:501:501:Asim El Baraka:/home/asim:/bin/bash

asim:~> grep 501 /etc/group
asim:x:501:
```
