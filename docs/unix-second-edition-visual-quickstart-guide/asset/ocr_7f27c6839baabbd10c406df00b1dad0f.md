# To make a hard link:

+   1. ls -l /home/deb/Projects/schedule/ -our* /home/helper/our*
+   To begin, list the files in both directories to make sure that the file to link exists and that there’s no other file with the intended name in the target directory. Here, we list the files that start with our in both /home/deb/Projects/schedule and in /home/helper. In this example, we’re verifying that the file does exist in Deb’s directory and that no matching files were found in the helper’s directory (Code Listing 2.14).

+   2. ln /home/deb/Projects/schedule/ -our.projects.latest /home/helper/our.projects
+   Here, ln creates a new file with a similar name in the helper’s home directory and links the two files together, essentially making the same file exist in two home directories.

+   3. ls -l /home/helper/o*
+   With this code, your helper can verify that the file exists by listing files that begin with o*. Now the file exists in two places with exactly the same content. Either user can modify the file, and the content in both locations will change.

# Tips

+   You can remove hard links just like you remove regular files, by using rm plus the filename. See the section called Removing Files with rm in this chapter.

+   If one user removes the file, the other user can still access the file from his or her directory.

+   Hard links work from file to file only within the same file system. To link directories or to link across file systems, you’ll have to use soft links, which are covered in the next section.

+   If you’re sneaky, you can use hard links to link directories, not just files. Make a new directory where you want the linked directory to be, and then use ln /home/whoever/existingdirectory/* /home/you/newdirectory/ to hard link all of the files in the old directory to the new directory. New files won’t be linked automatically, but you could use a cron job to refresh the links periodically—say, daily. See Chapter 9 for cron details.