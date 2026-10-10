+   C. type passv to force the FTP connection into passive mode
+   D. use mput instead of put to transfer the file

+   8. Users in your finance department are reporting errors when trying to connect to their server. You decide to monitor activity on this server as the users try to connect. What command would you use with dmesg to monitor these system events?
+   A. dmesg | tail -f
+   B. dmesg | less
+   C. dmesg | tail -n5
+   D. dmesg | less -h5

+   9. You have been asked to create a CD that contains the personal files of a user who is leaving your company. The files are stored on your Linux-based file server in /home/miranda and the CD needs to be readable on a Windows computer. What is the correct syntax to create the image file for the CD?
+   A. mkisofs -rW -o mirandasfiles.iso /home/miranda
+   B. mkisofs -rJ -o mirandasfiles.iso /home/miranda
+   C. mkisofs -r -o mirandasfiles.iso /home/miranda
+   D. cdrecord -rJ -o mirandasfiles.iso /home/miranda

+   10. You are managing Web servers in both a development environment and on the Internet (hostname is www). Once development on a given release is complete and tested, the developers ask you for a solution to keep the content on the staging server in the development environment synchronized with the content on the public Web server. What command would you run on the staging server to ensure that the files and all subdirectories on the staging server are updated on the public Web server as they are updated?
+   A. rsync * www:/home/httdocs
+   B. ftp www | put *
+   C. rsync -r * www:/home/httdocs
+   D. ssh www | copy -r * www:/home/httdocs

+   11. You have been asked to back up users' data on a particular server before a core application is upgraded. Because of the amount of data, you need to ensure that these files will fit on a remote hard disk. What command would you use to ensure that the smallest possible size of the backup file?