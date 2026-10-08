# Lesson 9

+   6. You may have made a mistake and do not need this new direc- tory. The storage directory should have contained a directory called storage. There are many ways for you to change this, but for this example we will look at using a tool to remove the unwanted directory, and create the new one when needed. To do this, what would you type?

Answer: rmdir HTML

+   7. To create a new directory named storage, type mkdir test. When you complete this step, type pwd and ls -1 to see what is in your current directory. Make sure you have the test directory created inside the directory you are currently located in. Once you ensure that this is good (you can walk back through the steps or the lessons in the book if you are having issues), your next step is to copy a file. You want to find a file in your current directory that you can copy to the test directory. If you are in your home directory, you may have a file to copy to another location. If you do not, move to another directory (using the cd command) and search for a file to copy. You can run a generic search by issuing a wildcard such as find /etc *.htm or find /etc *.conf as examples. You will see Unix perform the search and then list out at the end all the files you requested. Once you find a file you want to copy, what would you type to copy to the /etc/storage directory?

Answer: cp syslog.conf /etc/storage

If you wanted to verify that this copied over, the follow-up to this command would be

Answer: ls -1 /etc/storage

You should see that the file copied over. If not, check your work and go back through the steps just discussed.

> Unix Gone Wild You can specify more than one file with a path by using wildcards. A wildcard is a character that matches many characters. The * wildcard matches any number of characters.