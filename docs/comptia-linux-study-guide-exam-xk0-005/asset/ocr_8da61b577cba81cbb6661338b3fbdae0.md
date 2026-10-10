# Review Questions

+   5. A long-time server administrator has left the company, and now you are in charge of her system. Her old user account directory tree, /home/Zoe/, has been backed up. Which command is the best one to use to quickly remove her files and still indicate that you are removing the correct directory, but without forcing you to confirm every file deletion?
+      A. cp -R /home/Zoe/ /dev/null/
+      B. mv -R /home/zoe/ /dev/null/
+      C. rm -Rf /home/Zoe/
+      D. rm -ri /home/Zoe/
+      E. rm -rI /home/Zoe

+   6. There is a large directory structure that needs to be renamed. What mv command options should you consider employing? (Choose all that apply.)
+      A. -f
+      B. -i
+      C. -n
+      D. -r
+      E. -v

+   7. You are trying to decide whether to use a hard link or a symbolic link for a data file. The file is 5 GB, has mission-critical data, and is accessed via the command line by three other people. What should you do?
+      A. Create a hard link so that the file can reside on a different filesystem for data protection.
+      B. Create three hard links and provide the links to the three other people for data protection.
+      C. Create three symbolic links and protect the links from the three other people for data protection.
+      D. Create a symbolic link so that the file can reside on a different filesystem.
+      E. Create a symbolic link so that the links can share an inode number.

+   8. A short text-based control file is no longer working properly with the program that reads it. You suspect the file was accidentally corrupted by a control code update you performed recently, even though the file's control codes are all correct. Which command should you use next on the file in your problem investigation?
+      A. cat -v
+      B. cat -z
+      C. cat -n
+      D. cat -s
+      E. cat -E