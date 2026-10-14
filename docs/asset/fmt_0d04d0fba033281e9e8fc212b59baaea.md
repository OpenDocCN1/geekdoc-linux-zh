
14 matthew@seymour:~/empty$ export CDPATH=./usr
15 matthew@seymour:~/empty$ cd local
16 /home/mathew/empty/local
17 matthew@seymour:~/empty/local$

```bash
matthew@seymour:~$ chmod -c filename
```

```bash
matthew@seymour:~$ chmod 440 /etc/sudoers
```

```bash
matthew@seymour:~$ chmod 775 filename
```

```bash
matthew@seymour:~$ chmod 7755 directoryname
```

```bash
matthew@seymour:~$ getfacl filename
```

```bash
matthew@seymour:~$ setfacl -m u:sandra:rwx secrets.txt
```

```bash
matthew@seymour:~$ setfacl -r u:sandra: secrets.txt
```

```bash
matthew@seymour:~$ setfacl -m g:groupname:rwx secrets.txt
matthew@seymour:~$ setfacl -m o:r secrets.txt
```

```bash
matthew@seymour:~$ setfacl -m m:rx secrets.txt
```

```bash
matthew@seymour:~$ touch filename
```

```bash
matthew@seymour:~$ touch randomdirectory/newfile
```

```bash
matthew@seymour:~$ touch /home/matthew/randomdirectory/newfile
```

```bash
matthew@seymour:~$ touch /randomdirectory/newfile
```

```bash
matthew@seymour:~$ mkdir newdirectory
```

```bash
matthew@seymour:~$ mkdir music/newdirectory
```

```bash
matthew@seymour:~$ mkdir /home/matthew/music/newdirectory
```

```bash
matthew@seymour:~$ mkdir ~/music/newdirectory
```

```bash
matthew@seymour:~$ mkdir -p /music/newdirectory/subdir1/subdir2
```

```bash
matthew@seymour:~$ rmdir directoryname
```

```bash
matthew@seymour:~$ rmdir music/directoryname
```

```bash
matthew@seymour:~$ rmdir /home/matthew/music/directoryname
```

```bash
matthew@seymour:~$ rmdir ~/music/directoryname
```

```bash
matthew@seymour:~$ rm filename
```

```bash
matthew@seymour:~$ rm randomdirectory/filename
```

```bash
matthew@seymour:~$ rm /home/matthew/randomdirectory/filename
```

```bash
matthew@seymour:~$ rm -rf /randomdirectory/filename
```

```bash
matthew@seymour:~$ rm -r /home/matthew/randomdirectory/
```

```bash
matthew@seymour:~$ mv documents/filename archive
```

```bash
matthew@seymour:~$ mv oldfilename newfilename
```

```bash
matthew@seymour:~$ mv documents/oldfilename archive/newfilename
```

```bash
matthew@seymour:~$ mv /home/matthew/documents/oldfilename /home/matthew/archive/newfilename
```

```bash
matthew@seymour:~$ mv ~/documents/oldfilename ~/archive/newfilename
```

```bash
matthew@seymour:~$ cp documents/filename archive
```

```bash
matthew@seymour:~$ cp oldfilename newfilename
```

```bash
matthew@seymour:~$ cp documents/oldfilename archive/newfilename
```

```bash
matthew@seymour:~$ cp /home/matthew/documents/oldfilename /home/matthew/archive/newfilename
```

```bash
matthew@seymour:~$ cp ~/documents/oldfilename ~/archive/newfilename
```

```bash
matthew@seymour:~$ cat filename
```

```bash
matthew@seymour:~$ less filename
```

```bash
matthew@seymour:~$ rm -rf /
```

```bash
matthew@seymour:~$ sudo nano /etc/fstab
[sudo] password for matthew:
```

```bash
matthew@seymour:~$ shutdown -h now
[sudo] password for matthew:
matthew is not in the sudoers file. This incident will be reported.
```

```bash
root@seymour:~# mount -o rw,remount /
```

```bash
root@seymour:~# adduser admin
```

```bash
root@seymour:~# chmod 440 /etc/sudoers
```

```text
# This file MUST be edited with the 'visudo' command as root.
# Please consider adding content in /etc/sudoers.d/ instead of
# modifying this file.
# See the man page for how to write a sudoers file.
Defaults env_reset
Defaults secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
# Host alias
# User alias
# User privilege specification
root ALL=(ALL:ALL) ALL
# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL
# Allow members of group sudo to execute any command
%sudo ALL=(ALL:ALL) ALL
include /etc/sudoers.d
```

```bash
matthew@seymour:~$ adduser sandra
```

```bash
matthew@seymour:~$ sudo passwd sandra
Changing password for user sandra.
New password:
Retype password:
```
