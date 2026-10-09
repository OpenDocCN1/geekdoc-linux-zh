+   - man 5 updatedb.conf

The updatedb.conf file should include a directive to prune paths like /tmp/ and /media, among others. Given what you know about the FHS: Why do you think it's a good idea to prune these paths from the locate database? Why is it a good idea to prune filesystem types like nfs and proc?

# Task 2:

Now run:

+   - which which
+   - which locate
+   - whereis locate
+   - whereis updatedb
+   - whereis whereis

which shows you the absolute location of a given (relative) command, while whereis expands on this by showing other related files like config files, databases, and man pages.

# Notes:

Many common Linux tools are fairly complicated C programs; which is one exception. It is a short shell script which, with a bit of practice, you could understand in its entirety. Take a look at the /bin/which file and see how much of it makes sense to you!