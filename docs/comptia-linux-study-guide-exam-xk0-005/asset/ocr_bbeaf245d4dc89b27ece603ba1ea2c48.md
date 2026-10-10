+   3. Change the newly created file's owner and group to root by typing `sudo chown root:root /tmp/fileA.txt` and pressing Enter. If requested, enter the account's sudo password. The sudo and chown commands were covered in Chapter 15.
+   4. Next, you will create a small application using the nano text editor (covered in Chapter 4, "Searching and Analyzing Text"). Type `nano application.sh` and press Enter. This will put you into the nano text editor.
+   5. Type in the following, pressing the Enter key as needed:

```
#!/bin/bash
echo "Creating file /tmp/Activity.txt..."
echo "Hello World" > /tmp/Activity.txt
echo "Removing file..."
rm -ir /tmp/*.*
exit
```

+   6. Press `Ctrl+O` and then the Enter key to write out the text editor's buffer to the `activity.sh` file.
+   7. Press `Ctrl+X` to leave the text editor.
+   8. Run the application by typing `bash activity.sh` and pressing Enter.
+   9. When asked a question, type `y` at the prompt and press Enter. You should receive at least one error message relating to the attempt to delete the `/tmp/fileA.txt` file, but you may receive more error messages depending on what files and directories are currently located in the `/tmp/` directory.
+   10. Now you can begin the troubleshooting process. Since you ran the application, record your user account's name.
+   11. Document the action that causes the error to occur. (Hint: It was associated with the `/tmp/fileA.txt` file.)
+   12. Record the problem file's full directory reference. (Hint: Look at the previous step.)
+   13. Document that the application is not trying to launch any additional applications or employing local or remote services.
+   14. Display the problem file's directory's ownership, group membership, and various permissions by typing `ls -ld /tmp` and pressing Enter.
+   15. Record the directory's owner and its associated permissions.
+   16. Document the directory's group and its associated permissions.
+   17. Record the directory's other permissions. Note that if you see a `t` in the permissions, this refers to the sticky bit (covered in Chapter 15).
+   18. Determine which of the three directory permission sets (owner, group, or other) would apply to your user account and record it.