# v.4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

directory, which is what we are displaying here. Just as the default display for EXT file systems with fls is inode 2, the default for NTFS MFT record 5.

You can delve deeper into the file system by providing fls with a directory and it will display the contents of directory. For illustration, re run the command (use the up arrow and edit the previous command) with the MFT record 64 (the Users directory);

You can delve deep into each directory you wish. This is one way to "browse" the file system with fls.

We can also specify that fls only show us only "deleted" content on the command line with the option -d (only file entries) and -r (recursive) as well:

```
barry@forensic1:~/NTFS_Path_2017$ fls -o 2048 NTFS_Path_2017.E01 64
/d 65-144-2:
    AlbertE
/d 66-144-2:
    ElsaE
```

```
barry@forensic1:~/NTFS_Path_2017$ fls -o 2048 -Frd NTFS_Path_2017.E01
/r * 40-1238: Users/AlbertE/Documents/Credit Report.pdf
/r * 40-1238: Users/AlbertE/Documents/Credit Report.pdf:Zone.Identifier
/r-* 0: Users/AlbertE/Documents/ManProj/World's First Atomic Bomb Manhattan
Project Documentary - Films - YouTube.url
/r * 236-1238: Users/AlbertE/Documents/ManProj/MMhattan Project.docx
/r * 237-1238: Users/AlbertE/Documents/ManProj/The Manhattan Project
YouTube.url
/r * 238-1238: Users/AlbertE/Documents/ManProj/World's First Atomic Bomb
Manhattan Project Documentary - Films - YouTube.url
/r * 238-1238: Users/AlbertE/Documents/ManProj/Manhattan_project.zip
/r * 248-1238: Users/AlbertE/Documents/cyberbullying_by_proxy.doc
/r-* 0: Users/AlbertE/Pictures/Tails/Thumbs.db
/r * 221-228: Users/AlbertE/Pictures/Tails/Thumbs.db
/r * 216-228: Users/AlbertE/Pictures/Tails/BigBikeSiloCBR900SC33.jpg
/r * 218-228: Users/AlbertE/Pictures/Tails/BigBikeTailBandit.jpg
/r * 219-228: Users/AlbertE/Pictures/Tails/GemoTailK4.jpg
/r * 220-228: Users/AlbertE/Pictures/Tails/GemoTailUniversal.jpg
/r-* 0: Windows/Prefetch/EXPLORER.EXE-A806F497.pf
/r-* 0: Windows/Prefetch/MAINTENANCESERVICE.EXE-E411A328D.pf
d/ * 0: Windows/System32
/r * 167-228: Windows/Drop location 2.kml
/r * 168-228: Windows/Drop location 1.kml
/r * 169-228: Windows/Meeting_place.kml
/r * 170-228: Windows/Nums_to_use.txt
/r * 171-228: Windows/mycase.jpg
```

245