> So, if you see topics on the exam about how a user tried to execute a file in the current directory but couldn't, you know that the directory isn't in the path. The user should refer to the file with the full path from the root (/) or prefix the filename with ./ for the shortest method.

The path is usually set in the /etc/profile for all users or the ~/.bash_profile for an individual user. It's easy to alter the current path and add a directory without disrupting the previous path definitions. The following example shows how:

+   1.  Edit /etc/profile or .bash_profile.
+   2.  Navigate to the bottom of the file with the keystroke G.
+   3.  Open a new line for editing with the keystroke o.
+   4.  Add the following line, replacing yournewpath with the path that's correct for your system:

```
export PATH=$PATH:yournewpath
```

# # Getting $HOME

Some shortcuts and variables point to the user's home directory, and several utilities can take the user there quickly.

The HOME variable is read from the user's home directory entry in the /etc/passwd file. This variable's value is the full path to the current user's home directory:

cd $HOME – takes you to /home/username

Another method is using the cd command alone. This takes the user back home with the least number of keystrokes.

Finally, you can refer to the user's home directory with the tilde (~) character, so typing cd ~ gets the user home as well.

> The exam will test your ability to understand how a user can get home and what certain characters do for you. One of the most missed and misunderstood areas is the use of the ~username combination. Here's an example:
> 
> Your system has a user named tarfoo, and you logged in as the root user. There is a directory named /root/tarfoo on the system. Running the command cd ~tarfoo takes you to the tarfoo user's home directory, whereas running the command cd ~/tarfoo takes you to the /root/tarfoo directory.