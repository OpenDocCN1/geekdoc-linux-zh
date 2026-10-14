may use some configuration close to it, but with a few alterations. That's why you need to create a default test user and make sure everything works.

The default user should have the same privileges as any user, except that for security reasons you should lock the account when you're not testing it. The home directory's contents should be identical to what a new user gets. When you make changes to the default environment, unlock the test account, log in as the test user, and test the following:

+   - Try a bunch of file commands in /tmp.
+   - Make sure that both vi and emacs work.
+   - Send and receive mail.
+   - Run Netscape (with Java and JavaScript).

If all of these work properly, delete any new files you may have created (like a Mail or .netscape directory), lock the default user account again, and make sure the files that you just tested are the ones all new users get. Take a careful inventory of the files in the test user's home directory; tar them into an archive if you want.

# Default Permissions

The only question here is whether you should make home directories default to mode 700 with a umask of 077 (which creates files that only the user can read), or mode 755 with a umask of 022 (world-readable). In an ideal world, all new users would learn about permissions and chmod the first day they receive a Unix account. But since this is unrealistic, you need to make a decision about what type of users you have. Certainly, email and Netscape caches should stay unreadable (these programs take care of that), but what about other files?

If, for example, you have an academic system with both professors and students, the professors probably want world read access turned off from day one. However, they may require group read access for collaborative efforts. On the other hand, users of a small company's network may not have to worry about students getting a sneak preview of next Friday's exam, and may find it counterproductive not to have complete access to all work files.

# Commands in Shell Startup Files

People tend to do too much with commands in shell startup files (that is, check certain parameters on the machine or setup files). This cripples startup speed, which can lead to all kinds of frustration (see Section 9.4, on tcsh and csh). Large shell scripts also slow down shell interaction. Each command in a shell startup file requires creating a new process, loading and executing the program, and transferring the exit status. If you