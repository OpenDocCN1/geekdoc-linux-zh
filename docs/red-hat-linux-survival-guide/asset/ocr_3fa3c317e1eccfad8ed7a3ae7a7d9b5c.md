+   1. Create a subdirectory in the ~ftp directory for uploads. This directory is typically called incoming, and so I use this name here.
+   
+   2. Add the following line in your /etc/ftpaccess file:
+   ```
+   upload /home/ftp /incoming yes root ftp 0600 nodirs
+   ```
+   
+   3. Make sure that you change /home/ftp to the appropriate directory. For example, if your ~ftp is really /data/ftp, then change /home/ftp to /data/ftp in the preceding line. Also, if you want to allow anonymous users to be able to create subdirectories under ~ftp/incoming, remove the nodirs option in the preceding line.
+   
+   4. Run the following commands:
+   ```
+   chown -R root.ftp ~ftp/incoming
+   chmod -R 1733 ~ftp/incoming
+   ```
+   The chown command sets root as the owner and ftp as the group for the incoming directory. The chmod command changes the incoming directory permissions such that root has read, write, and execute (rwx) permissions and the group and the world have write and execute (wx) permissions. It also sets the sticky bit for the directory and all its files. See the nearby sidebar for more info on the sticky bit.
+   
+   5. Finally, make sure that you have the anonymous user type listed in at least one of the class definitions in your /etc/ftpaccess file. By default real, guest, and anonymous are all included in the default “all” class, so you do not need to do anything unless you have altered the default class definitions.

# "Hand me one of them sticky bits..."

The sticky bit protects the files from being deleted by regular users. Normally when a directory has write and execute permissions set for everyone, any user of that system can delete a file in that directory. The sticky bit stops that by allowing only the creator of the file to delete the file. Because the FTP server writes the file setting root being the owner, no one but root is allowed to delete the uploaded files.