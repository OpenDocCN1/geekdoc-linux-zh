+   2. At the session prompt, enter `cd /tmp`.
+   3. Create a directory named **HideMe** by entering `mkdir HideMe` at the session prompt.
+   4. Make the HideMe directory restricted from anyone but root or the root group by entering `chmod 640 ./HideMe`.
+   5. Enter `exit`.

Try to access the HideMe directory as the student user by completing the following steps:

+   1. At the session prompt, enter `cd /tmp`.
+   2. Generate a listing of the contents of `/tmp` by entering `ls |more`.

Do you see the HideMe directory displayed?

You should be able to view the directory.

Now try changing to the HideMe directory by entering `cd /tmp/HideMe`.

Were you able to change to the HideMe directory? Why or why not?

You should receive a message indicating that you don’t have the appropriate permissions to access the directory.

Execute a script file by completing the following steps:

+   1. Change back to the root user account by entering `su -` and entering a password of **novell**.
+   2. Change to the `/tmp` directory by entering `cd /tmp`.
+   3. At the shell prompt, enter `ls scriptfile.txt`.
+   4. You should see the `scriptfile.txt` file you created in the previous chapter. This file contains a series of commands that can be executed from within the file. If you skipped that exercise, go back now and create the text file according to the lab instructions.
+   5. Verify that `scriptfile.txt` contains the correct commands by entering `cat ./scriptfile.txt`. You should see the commands you entered in the previous exercise.
+   6. Try to execute the file by entering `./scriptfile.txt`.

What happens? Why?

You should see a message indicating that permission to run the file is denied. This happens because the Execute permission has not been granted.