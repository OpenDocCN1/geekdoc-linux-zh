
6. At the command prompt, type `cd mysamples` and press Enter. Next, type `ls -F` at the command prompt and press Enter. Notice that the sample1 file you moved in Step 5 was moved here.

7. At the command prompt, type `mv sample4 ..` and press Enter. Next, type `ls -F` at the command prompt and press Enter. How many files are there, and what are their names? Where did the sample4 file go?

8. At the command prompt, type `cd ..` and press Enter. Next, type `ls -F` at the command prompt and press Enter to view the new location of sample4.

9. At the command prompt, type `mv sample4 mysamples/sample2` and press Enter. What message appeared on the screen and why?

10. Type y and press Enter to confirm you want to overwrite the file in the destination folder.

11. At the command prompt, type `mv sample2 mysamples` and press Enter. Type y and press Enter to confirm you want to overwrite the file sample3 in the destination folder.

12. At the command prompt, type `ls -F` and press Enter. How many files are there and why?

13. At the command prompt, type `mv sample1* mysamples` and press Enter. Type y and press Enter to confirm you want to overwrite the file sample1B in the destination directory.

14. At the command prompt, type `ls -F` and press Enter. Notice that there are no sample files in the /root directory.

15. At the command prompt, type `cd mysamples` and press Enter. Next, type `ls -F` at the command prompt and press Enter. Notice that all files originally in /root have been moved to this directory.

16. At the command prompt, type `cd ..` and press Enter. Next, type `ls -F` at the command prompt and press Enter. Type `mv mysamples samples` and press Enter. Next, type `ls -F` at the command prompt and press Enter. Why did you not need to specify the recursive option to the mv command to rename the mysamples directory to samples?

17. Type exit and press Enter to log out of your shell.

## Project 4-4

In this hands-on project, you make and view links to files and directories.

1. Switch to a command-line terminal (tty2) by pressing Ctrl+Alt+F2 and log in to the terminal using the user name of root and the password of LNXrocks!.

2. At the command prompt, type `cd samples` and press Enter. Next, type `ls -F` at the command prompt and press Enter. What files do you see? Next, type `ls -l` at the command prompt and press Enter. What is the link count for the sample1 file?

3. At the command prompt, type `ln sample1 hardlinksample` and press Enter. Next, type `ls -F` at the command prompt and press Enter. Does anything in the terminal output indicate that sample1 and hardlinksample are hard-linked? Next, type `ls -l` at the command prompt and press Enter. Does anything in the terminal output indicate that sample1 and hardlinksample are hard-linked? What is the link count for sample1 and hardlinksample? Next, type `ls -li` at the command prompt and press Enter to view the inode numbers of each file. Do the two hard-linked files have the same inode number?

4. At the command prompt, type `ln sample1 hardlinksample2` and press Enter. Next, type `ls -l` at the command prompt and press Enter. What is the link count for the files sample1, hardlinksample, and hardlinksample2? Why?

5. At the command prompt, type `vi sample1` and press Enter. Enter a sentence of your choice into the vi editor, and then save your document and quit the vi editor.

6. At the command prompt, type `cat sample1` and press Enter. Next, type `cat hardlinksample` at the command prompt and press Enter. Next, type `cat hardlinksample2` at the command prompt and press Enter. Are the contents of each file the same? Why?

7. At the command prompt, type `ln -s sample2 symlinksample` and press Enter. Next, type `ls -F` at the command prompt and press Enter. Does anything in the terminal output indicate that sample2 and symlinksample are symbolically linked? Which file is the target file? Next, type `ls -l` at the command prompt and press Enter. Does anything in the terminal output indicate that sample2 and symlinksample are symbolically linked? Next, type `ls -li` at the command prompt and press Enter to view the inode numbers of each file. Do the two symbolically linked files have the same inode number?

8. At the command prompt, type `vi symlinksample` and press Enter. Enter a sentence of your choice into the vi editor, and then save your document and quit the vi editor.

9. At the command prompt, type `ls -l` and press Enter. What is the size of the symlinksample file compared to sample2? Why? Next, type `cat sample2` at the command prompt and press Enter. What are the contents and why?

10. At the command prompt, type `ln -s /etc/sysconfig/network-scripts net-scripts` and press Enter. Next, type `ls -F` at the command prompt and press Enter. What file type is indicated for net-scripts? Next, type `cd net-scripts` at the command prompt and press Enter. Type `pwd` at the command prompt and press Enter to view your current directory. What is your current directory? Next, type `ls -F` at the command prompt and press Enter. What files are listed? Next, type `ls -F /etc/sysconfig/network-scripts` at the command prompt and press Enter. Note that your net-scripts directory is merely a pointer to the /etc/sysconfig/network-scripts directory. How can this type of linking be useful?

11. Type `exit` and press Enter to log out of your shell.

## Project 4-5

In this hands-on project, you find files on the filesystem using the **find**, **locate**, and **which** commands.

1. Switch to a command-line terminal (tty2) by pressing Ctrl+Alt+F2 and log in to the terminal using the user name of **root** and the password of LNXrocks!.

2. At the command prompt, type `touch newfile` and press Enter. Next, type `locate newfile` at the command prompt and press Enter. Did the `locate` command find the file? Why?

3. At the command prompt, type `updatedb` and press Enter. When the command is finished, type `locate newfile` at the command prompt and press Enter. Did the `locate` command find the file? If so, how quickly did it find it? Why?

![](img/c27875544958897d817484d558c208c8_206_0.png)

4. At the command prompt, type `find / -name "newfile"` and press Enter. Did the `find` command find the file? If so, how quickly did it find it? Why?

5. At the command prompt, type `find /root -name "newfile"` and press Enter. Did the `find` command find the file? How quickly did it find it? Why?

6. At the command prompt, type `which newfile` and press Enter. Did the `which` command find the file? Why? Type `echo $PATH` at the command prompt and press Enter. Is the /root directory listed in the PATH variable? Is the /bin directory listed in the PATH variable?

7. At the command prompt, type `which grep` and press Enter. Did the `which` command find the file? Why?

8. At the command prompt, type `find /root -name "sample"` and press Enter. What files are listed? Why?

9. At the command prompt, type `find /root -type l` and press Enter. What files are listed? Why?

10. At the command prompt, type `find /root -size 0` and press Enter. What types of files are listed? Type `find /root -size 0 | more` to see all of the files listed.

11. Type `exit` and press Enter to log out of your shell.

## Project 4-6

In this hands-on project, you delete files and directories using the `rmdir` and `rm` commands.

1. Switch to a command-line terminal (tty2) by pressing Ctrl+Alt+F2 and log in to the terminal using the user name of `root` and the password of LNXrocks!.

2. At the command prompt, type `cd samples` and press Enter. At the command prompt, type `ls -R` and press Enter. Note the two empty directories todottles and undermysamples.

3. At the command prompt, type `rmdir undermysamples` and press Enter. Did the command work? Why? Next, type `ls -F` at the command prompt and press Enter. Were both directories deleted successfully?

4. At the command prompt, type `rm sample1*` and press Enter. What message is displayed? Answer n to all three questions.

5. At the command prompt, type `rm -f sample1*` and press Enter. Why were you not prompted to continue? Next, type `ls -F` at the command prompt and press Enter. Were all three files deleted successfully?

6. At the command prompt, type `cd ..` and press Enter. Next, type `rmdir samples` at the command prompt and press Enter. What error message do you receive and why?

7. At the command prompt, type `rm -Rf samples` and press Enter. Next, type `ls -F` at the command prompt and press Enter. Was the samples directory and all files within it deleted successfully?

8. Type `exit` and press Enter to log out of your shell.
