Canyon, and country music singers from the Internet and put them on my system login screen.

+   1. Once more, let’s go into our favorite editor and modify /etc/dt/config/C/Xresources.

+   2. Go to the MISC area. Here we’ll find the following lines:

!!Dtlogin*logo*bitmapFile: < bitmap or pixmap file >

+   3. Delete the leading !!, which are the comment designators.

+   4. Replace < bitmap or pixmap file > with the name of the bitmap file using the entire path location. The line should look as follows:

Dtlogin*logo*bitmapFile: /usr/lib/X11/bitmap/cake.bm

+   5. Save the file.

+   6. Now log out and back in. We should see the birthday cake in the login screen. Again, we didn’t need to “reload” the file, because the act of logging out and back in does that task.

Now that we’ve seen how easily we can make some simple customizations in CDE for our end users, we should be able to take this knowledge and really make their CDE environments a productive and friendly place to work.

# CDE - Advanced Topics

# The Relationship among X, Motif, and CDE

X, OSF/Motif, and CDE are enabling framework technologies. Taken together, X, Motif, and CDE make up the three graphical layers on top of the operating system and the hardware platform.