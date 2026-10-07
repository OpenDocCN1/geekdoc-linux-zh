# v.4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

point. That's a lot of files, for the sake of this exercise let's just look at the contents of the user Albert's Pictures directory (use the same command, but **grep** for AlbertE/Pictures):

```
barry@forensic1:~/NTFS_Pract_2017$ find /mnt/evid/ -type f | grep
"AlbertE/Pictures"
/mnt/evid/Users/AlbertE/Pictures/b45ac80a965617dd71e32851c47f3_refined.jpg
/mnt/evid/Users/AlbertE/Pictures/bankor1.jpg
/mnt/evid/Users/AlbertE/Pictures/desktop.ini
/mnt/evid/Users/AlbertE/Pictures/fighterama2005-ban3.jpg
/mnt/evid/Users/AlbertE/Pictures/jet.mpg <<< Pay attention to this one
/mnt/evid/Users/AlbertE/Pictures/pvorden2.jpg
...
```

Of particular interest in this output is the jet.mpg. Take note of this file. Our current method of listing files shows us the expected file type. It is an MPEG video. You can play the video with the **mplayer** command from the command line to view it you like.

```
barry@forensic1:~/NTFS_Pract_2017$ file /mnt/evid/Users/AlbertE/Pictures/jet.jpg
/mnt/evid/Users/AlbertE/Pictures/jet.mpg: MPEG sequence, v1, progressive Y'CbCr 4:2:0 video, CIF NTSC, NTSC 4:3, 29.97 fps, Constrained
```

```
barry@forensic1:~/NTFS_Pract_2017$ mplayer /mnt/evid/Users/AlbertE/Pictures/jet.mpg
<video plays>
Playing /mnt/evid/Users/AlbertE/Pictures/jet.mpg.
...
```

At this point we finished with the mount point and the fused image. Keeping track of mounted disks and partitions is an important part of this process:

```
barry@forensic1:~/NTFS_Pract_2017$ su -
Password:
root@forensic1:~# umount /mnt/evid && fusermount -u /mnt/evid
root@forensic1:~# exit
logout
barry@forensic1:~/NTFS_Pract_2017$
```

249