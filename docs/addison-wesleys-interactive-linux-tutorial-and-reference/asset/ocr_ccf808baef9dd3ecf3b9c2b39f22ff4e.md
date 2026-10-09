If the system accepts your new password, you will see a screen similar to Figure 3-6.

```
$passwd
Changing password for david
Old password:
New Password:
Re-enter new password:
Password update successful
$
|
```

# Figure 3-6 System Confirms Change of Password

The password requirements that we outlined in the CBT course apply here, of course. In addition, the new password must differ from the old password by at least three characters, and it must not be similar to your *userid*. If the new password that you select does not meet system guidelines, you will get an error message that tells you why the new password is unacceptable. After a few unsuccessful attempts at changing your password, the system will kick you back to the shell prompt, and you will have to begin again.

+   8.  In the CBT course, we introduced the file named `.profile`, and we told you that you can use this file to customize your Linux environment. (In some shells, this file is named `.login`.) Find out whether the file `.profile` exists in your Linux account. Although we're getting a little ahead of ourselves with this next exercise, think of this as a preview of coming attractions.

+   a.  At the shell prompt on your terminal:
+   
+   Type `ls .profile`
+   
+   (Be sure to leave a space after `ls`.) The `ls` command means “list the file.” Adding `.profile` to the command tells Linux to list the file named `.profile`.

+   b.  Press <Enter>
+   
+   Linux will respond with a screen similar to either Figure 3-7 or Figure 3-8.