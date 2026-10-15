
The next five examples will use Python standard library modules and embed Bourne shell commands in a Python "wrapper" (UNIX shell command(s) embedded in Python code), primarily using os.system, to

- 1. Back up a single file on the hard disk to a mounted USB thumb drive
- 2. Back up a single directory beneath your home directory on the hard disk to a directory on a mounted USB thumb drive
- 3. Back up a single directory beneath your home directory on the hard disk to another network location on your local area network in Push mode
- 4. Back up a directory on the hard disk to a mounted USB thumb drive in a rolling, incremental scheme that creates "snapshots" of the source directory anytime the Python script is run
- 5. Customize a system command to show permissions of files in the current working directory that match a certain pattern

The following simple example shows you how to use Python to back up a single file on your hard disk to the USB thumb drive you mounted and attached to your system’s file system in Example 16.26. It assumes you have an ordinary file in the current working directory named rsynctest, and that the destination path on the USB thumbdrive is /usr/home/bob/USBint.

## Example 16.27

```
>>>import os
>>>os.system('rsync -av rsynctest /usr/home/bob/USBint')
sending incremental file list
rsynctest
sent 192 bytes received 35 bytes 454.00 bytes/sec
total size is 92 speedup is 0.41
>>>
```

The following example shows you how to use Python to back up an entire directory on your hard disk to the USB thumb drive you mounted and attached to your system’s file system in Example 16.26. It assumes you have a directory under the current working directory named syncdir, and that the destination path on the USB thumb drive is /usr/home/bob/USBint.

## Example 16.28

```
>>>import os
>>>os.system('rsync -av syncdir /usr/home/bob/USBint')
sending incremental file list
syncdir/
syncdir/Chap16.doc
syncdir/backup1.py
syncdir/ossystem.py

sent 280,176 bytes received 77 bytes 186,835.33 bytes/sec
total size is 279,855 speedup is 1.00
0
>>>
```

The following example shows you how to use Python to back up an entire directory on your hard disk to a remote location on your local area network. It assumes:

- 1. You have the ssh daemon running on both your local and remote host
- 2. You have a directory under the current working directory named syncdir2 with some files in it
- 3. Where a password is asked for, you type in your password on the remote host
- 4. That the destination path to the remote host is bob@192.168.0.7:/Users/b/unix3e

## Example 16.29

```
>>import os
>>os.system('rsync -av -e ssh syncdir2 bob@192.168.0.7:/Users/b/unix3e')
The authenticity of host '192.168.0.7 (192.168.0.7)' can't be established.
RSA key fingerprint is 64:62:9c:46:2a:ef:ba:7d:45:02:40:6e:b5:7e:f2:f5.
No matching host key fingerprint found in DNS.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.0.7' (RSA) to the list of known hosts.
Password:
building file list ... done
syncdir2/
syncdir2/Chap16.doc
syncdir2/backup1.py
syncdir2/ossystem.py

sent 280,171 bytes received 96 bytes 16,985.88 bytes/sec
total size is 279,855 speedup is 1.00
0
>>>
```

## EXERCISE 16.15

- 1. Repeat the operations shown in Examples 16.16 through 16.29, substituting file names and directory paths on your computer system and local network for those shown in the examples. When backing up files to a USB thumb drive is finished,

be sure to unmount that drive before removing it from the USB connector on your machine.

The following example shows you how to create a rolling backup scheme of “snapshots” of a directory on your hard disk, and archive the contents of the directory to multiple (five) backup directories on the USB thumb drive you mounted and attached to your system’s file system in Example 16.26. It is assumed that the source directory containing some files exists. Every time you execute this Python script, it recycles the oldest (fifth) archived directory, and creates a new full backup with the rsync command:

## Example 16.30

```
#!/usr/local/bin/python
import os
import shutil
target = "/usr/home/bob/USBint/"
i = 1
while i <= 5:
    temp_path = target + str(i) + "/"
    if not os.path.exists (temp_path):
        try:
            os.makedirs (temp_path)
            print "Created " + temp_path
        except:
            print " Could not create " + temp_path
    i = i + 1
print "Deleting the oldest archive"
shutil.rmtree (target + "5")
print "Recycle the backups"
os.rename (target + "4", target + "5")
os.rename (target + "3", target + "4")
os.rename (target + "2", target + "3")
# Unlike some other rolling snapshot schemes that use cp -al,
    we do full
#backup copies across devices, filesystems, etc. with the following-
os.system('cp -a ' + target + "1" + " " + target + "2")
os.system('rsync -av /usr/home/bob/python/' + " " + target + "1")
```

Here is another example of carrying out simple system administration using Python. It customize a shell command to show permissions set on files in the current working directory that match a certain pattern:

## Example 16.31

```
#!/usr/local/bin/python
import stat, sys, os, string, commands
```
