# APPLY YOUR KNOWLEDGE

+   2. Locate all files using the find command, and transfer them to tape using cpio:
```
find . -mtime -30 -print | cpio -oB > \
/dev/rmt/0
```
3. List all the files that were backed up in step 2:
```
cpio -ict < /dev/rmt/0
```
4. Use the pax utility to list the contents of the tape that was created using cpio:
```
pax -v -f /dev/rmt/0
```

# 11.3 Using ufsdump and ufsrestore

In this exercise, you’ll use the ufsdump command to back up an entire file system. You’ll then use the ufsrestore command to restore a file.

Caution: Don’t do this exercise on a production system.

Estimated Time: 20 minutes

+   1. Log in as root.
2. Back up the entire /var file system to tape as follows:
```
ufsdump 0ucf /dev/rmt/0 /var
```
3. Remove the /var/adm/messages file:
```
rm /var/adm/messages
```
4. Restore the /var/adm/messages file using ufsrestore:
```
cd /var
ufsrestore -ivf /dev/rmt/0
```
5. At the ufsrestore> prompt, verify that the messages file is on the tape:
```
ls adm/messages
```

+   6. Mark the file for extraction, and then extract the file:
```
add adm/messages
extract
```
When the system asks you to “Specify the next volume”, type 1.
When asked to “set owner/mode for ‘.’?[yn]”, enter y
Enter q to exit the ufsrestore utility.

7. Verify that the file has been restored to its proper location using the ls -l command.

# Review Questions

+   1. What will the following command sequence do?
```
#cd /home/my junk
#tar cvf /dev/rmt/0 .
```
A. Take all the files in /home/my junk, package them into a single tar archive on /dev/rmt/0, and print out a commentary of the process.
B. Extract the contents of the tape at /dev/rmt/0 to /home/my junk.
C. Tar all the files in /dev/rmt/0 to /home/my junk, create a table of contents, and ignore checksum errors.
D. Tar all the files in the current directory into two separate archives, one for the contents of my junk and one for the rest of /home.

2. Given the following backup schedule, which tapes would be needed to fully restore the system if it goes down on a Saturday?
• First Monday of the month—level 0 (tape 1)