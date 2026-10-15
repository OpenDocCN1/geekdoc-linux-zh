other things. Pay no attention. Finally, you may be asked what kind of terminal you're on. Chances are good you can just take whatever the default is and get down to your business. But if you see a bunch of funny stuff on your screen, or the keyboard seems to be behaving peculiarly, it's a good bet that something went wrong somewhere and the default is not going to be good enough.

# 2. How long can a UNIX filename be and what characters can it include?

UNIX filenames are much more flexible than, say, DOS filenames. At the very least, they can be 14 characters long on even the oldest systems, and these days most UNIX systems will support a file called reallyridiculouslylong-andcomplex.filename. But that is probably not a particularly useful filename. The only hard and fast rule for filenames is that they can include any character except a slash (/).

# 3. What is a good UNIX filename?

Realistically, you should probably limit your filenames to the following:

+   - alphanumeric characters
+   - underscores
+   - periods

Other characters may work on your version of UNIX, but may not translate very well to other systems.

# 4. How can I change a file's mode or permissions?

Use chmod. This command, which is short for "change mode," lets you easily change any file you own so that only those people you authorize can read it, change it, or execute it. There are three basic levels of users, as we saw above: the owner (user) of the file, the owner's group, and everyone else (others). And there are three levels of permissions: read, write, and execute. The types of users are abbreviated "u" for user, "g" for the owner's group, and "o" for all those other