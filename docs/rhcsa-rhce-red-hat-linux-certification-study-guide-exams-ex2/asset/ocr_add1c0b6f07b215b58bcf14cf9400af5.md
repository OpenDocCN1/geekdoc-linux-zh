# SELF TEST ANSWERS

# Basic File Permissions

+   1. The command that configures read and write permissions on the file named question1 in the local directory, with no permissions for any other user is:
+   
+   ```
+   # chmod 600 question1
+   ```
+   
+   2. The single command that changes the user owner to professor and group owner to assistants for the noted file is:
+   
+   ```
+   # chown professor.assistants question2
+   ```
+   
+   It's acceptable to substitute a colon (:) for the dot (.).
+   
+   3. The command that change the attributes of a file named question3 to allow you to only add to that file is:
+   
+   ```
+   # chattr +a question3
+   ```

# Access Control Lists and More

+   4. The command that adds ACLs to the mount of the /dev/sda2 partition on the /home directory is:
+   
+   ```
+   # mount -o remount,acl /dev/sda2 /home
+   ```
+   
+   Since you don't know whether the filesystem is configured in /etc/fstab, you need the device and directory for the command.
+   
+   5. The command that reads current ACLs for the local file named question5 is:
+   
+   ```
+   # getfacl question5
+   ```
+   
+   6. The single command gives that members of the group named managers read access to the project6 file in the /home/project directory is:
+   
+   ```
+   # setacl -m g:managers:r /home/project/project6
+   ```
+   
+   7. The command that prevents members of the group named temps from having any access to the secret7 file in the /home/project directory is:
+   
+   ```
+   # setacl -m g:temps:--- /home/project/secret7
+   ```