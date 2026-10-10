+   4. At the command prompt, type `ln sample1 hardlinksample2` and press Enter. Next, type `ls -1` at the command prompt and press Enter. What is the link count for the files sample1, hardlinksample1, and hardlinksample2? Why?

+   5. At the command prompt, type `vi sample1` and press Enter. Enter a sentence of your choice into the vi editor, and then save your document and quit the vi editor.

+   6. At the command prompt, type `cat sample1` and press Enter. Next, type `cat hardlinksample` at the command prompt and press Enter. Next, type `cat hardlinksample2` at the command prompt and press Enter. Are the contents of each file the same? Why?

+   7. At the command prompt, type `ln -s sample2 symlinksample` and press Enter. Next, type `ls -F` at the command prompt and press Enter. Does anything in the terminal output indicate that sample2 and symlinksample are symbolically linked? Which file is the target file? Next, type `ls -1` at the command prompt and press Enter. Does anything in the terminal output indicate that sample2 and symlinksample are symbolically linked? Next, type `ls -11` at the command prompt and press Enter to view the inode numbers of each file. Do the two symbolically linked files have the same inode number?

+   8. At the command prompt, type `vi symlinksample` and press Enter. Enter a sentence of your choice into the vi editor, and then save your document and quit the vi editor.

+   9. At the command prompt, type `ls -1` and press Enter. What is the size of the symlink-sample file compared to sample2? Why? Next, type `cat sample2` at the command prompt and press Enter. What are the contents and why?

+   10. At the command prompt, type `ln -s /etc/sysconfig/network-scripts net-scripts` and press Enter. Next, type `ls -F` at the command prompt and press Enter. What file type is indicated for netscripts? Next, type `cd netscripts` at the command prompt and press Enter. Type `pwd` at the command prompt and press Enter to view your current directory. What is your current directory? Next, type `ls -F` at the command prompt and press Enter. What files are listed? Next, type `ls -F /etc/sysconfig/network-scripts` at the command prompt and press Enter.  
+   Note that your netscripts directory is merely a pointer to the /etc/sysconfig/network-scripts directory. How can this type of linking be useful?

+   11. Type `exit` and press Enter to log out of your shell.

# Project 4-5

In this hands-on project, you find files on the filesystem using the **find**, **locate**, and **which** commands.

+   1. Switch to a command-line terminal (try2) by pressing Ctrl+Alt+F2 and log in to the terminal using the user name of **root** and the password of LNKr0cks!.

+   2. At the command prompt, type `touch newfile` and press Enter. Next, type `locate newfile` at the command prompt and press Enter. Did the `locate` command find the file? Why?

+   3. At the command prompt, type `updatedb` and press Enter. When the command is finished, type `locate newfile` at the command prompt and press Enter. Did the `locate` command find the file? If so, how quickly did it find it? Why?

![](bbox=[0.85, 0.25, 0.95, 0.28])