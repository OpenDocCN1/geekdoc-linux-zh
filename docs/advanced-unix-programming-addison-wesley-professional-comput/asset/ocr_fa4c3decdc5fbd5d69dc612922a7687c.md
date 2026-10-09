# 5.12 Setting User and Group IDs

The rules for how the real and effective user and group IDs can be changed are complicated, and different depending on whether the process is running as super-user. Before explaining the rules, I need to note that in addition to its current real and effective user and group IDs, the kernel keeps for each process a record of the *original* effective user and group IDs that were set by the last *exec*. These are called the *saved set-user-ID* and *saved set-group-ID*.

Here now are the rules for setting user IDs; group IDs have similar rules:

+   1. Other than by an *exec* (which can change the saved ID), an ordinary (non-superuser) process can never explicitly change the real user ID or saved ID.
+   2. An ordinary process can change the effective ID to the real or saved ID.
+   3. A superuser process can change the real and effective user IDs to any user-ID value.
+   4. When a superuser process changes the real user ID, the saved ID changes to that value as well.

The superuser rules aren't that interesting—anything goes. The two rules for ordinary users essentially mean this: If an *exec* causes the real and effective user-IDs (or group IDs) to be different, the process can go back and forth between them.

Here's one scenario where going back and forth is useful: Imagine a utility *putfile* that transfers files between computers on a network. The utility needs access to a log file that only the administrative user (call it *pfadm*) can access. The program file is owned by *pfadm*, with the set-user-ID bit on. It starts running and can access the log file, since its effective user ID is *pfadm*. Then, to write the real user's files, it sets the effective user ID to the real user ID so that the real user's permissions will control the access. When it's done, it sets the effective user ID back to *pfadm* to access the log file again. (If the original effective user ID weren't saved, it wouldn't be able to go back.) Note that while it sounds like *pfadm* is special as far as this utility goes, it is just an ordinary user to the kernel—not a superuser.

Now for the calls themselves. The only useful ones for ordinary-user processes are *seteuid* and *setegid*.