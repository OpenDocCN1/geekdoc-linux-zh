numeric. They both accomplish the same thing, so use the one you feel comfortable with.

+   - **chown**—Only the super-user can change who owns a file. If you can convince your administrator to do so, chown changes the owner. Reasons why you might not want to try are covered in Lesson 20, "Privileged Commands."
+   - **chgrp**—You can change the group that a file belongs to with the chgrp function. You can only change the file to a group that you belong to.
+   - **newgrp**—Rather than constantly having to change the group for files you create, you can use newgrp to log in to a group of which you are a member. All files that are created for the remainder of your login session are created under that group.
+   - **su**—The substitute user command effectively switches to another user within a single login session. If you have the password of another account, you can use su to perform operations under this account. Any files you create are owned by this user.