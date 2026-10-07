# A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

This command uses wget to download the catdocx script from github directly to /usr/bin/catdocx (with the -o option). The && allows us to run chmod immediately after the wget completes to change the permissions and make the file executable.

Now we can re-run the icat command used earlier on the MFT entry pointing to the Uranium-235 keyword. Then we will re-direct the output of icat to a file called NTFS.236. Then we use catdocx piped through less to display the file:

```
barry@forensic1:~$ icat -o 2048 ../NTFS_Pract_2017/NTFS_Pract_2017.E01 236 =
NTFS.236
```

barry@forensic1:~$ catdocx NTFS.236 | less
Watch modern marvels the Manhattan project. You can find it in 5 spots on youtube
https://www.youtube.com/watch?v=SwHdlsany9Y
https://www.youtube.com/watch?v=VGGAIuc5WI
https://www.youtube.com/watch?v=HvugtVOP6
https://www.youtube.com/watch?v=aXY5V-zRyc
https://www.youtube.com/watch?v=aJuBHzgLUaW
------------------------------------
Modern Marvels: Manhattan Project

What is the difference between Uranium-235 and Uranium-238?

# Physical Carving

We've seen a number of cases in previous exercises where we needed to locate headers to recover data. We saw a specific need for this with the ext4 exercise where we found that block pointers are no longer available for deleted files, making recovery very difficult. We also did manual recovery in our "Data Carving with dd", locating the header of a JPEG file in hex and using dd to physically "carve" the out. A useful skill, but a bit tedious on a large disk with potentially dozens, hundreds or even thousands of files that might require recovery. If you are unfamiliar with file carving, or need a refresher, you can start reading here: http://forensicwiki.org/wiki/File_Carving

Since we gained a courtesy understanding of the mechanics of carving through our dd problem, we can move on more automated tools that do the work for us. There are a number of tools available to accomplish this. We are going to concentrate on just two Scalpel, and photorec. The latter is from the testdisk package.