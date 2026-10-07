# v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

Desktop/Documents/Evidence/winlog.txt

```
barry@forensic1:-$ cat filelist.txt
```

Desktop/Documents/Evidence/winlog.txt

In the above session, we've used the tee command to both display the output of the ls command to the screen, send it to a file called filelist.txt. In the context of the forensic examination, this is useful to capture the output of tools in a file (remember to use >> append).

String multiple powerful commands together is one of the most useful and powerful techniques provided by Linux for forensic analysis. This is one of the single most important concepts you will want to learn if you take on Linux as a forensic tool. With a single command line built from multiple commands and pipes, you can use several utilities and programs to build an analysis very quickly.

# File Attributes

Linux file systems (like ext2, ext3, ext4) support what are called file attributes. There are a few of them, and we will not cover all of them. There are two that can be very useful for protecting forensic data from haphazard deletion and tampering. These are append only (a) and immutable (i).

Attributes are flags that control what file operations are allowed to occur on a file directory. Some of them can be changed, and some cannot. We can list the attributes of files and directories in our current directory with lsattr

```
root@forensic1:/MyDirectory# lsattr
------e /data
------e /textfile.txt
------e /file1.txt
------e /log.txt
```

I have a directory, in my /home/$USER directory (specified by ~/$DIRNAME in the prompt). This output shows that all of the available attributes, the files and single directory (data is a directory) all have only the extents attribution (e). We will not cover

> "Extents are a method of mapping physical blocks of data in a contiguous fashion."