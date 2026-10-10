**Note:** If a weak password is chosen, a warning message will appear. However, since the command is run with root privileges the weak password is allowed.

+   13.  Type the command: `su -c 'passwd dbadmin1'` and press <enter>.
+   14.  Password: ISS316$Security
+   15.  A prompt will appear for dbadmin's new password. Enter the password: lab3 and press <enter>
+   16.  Enter the password lab3 again to confirm. Press enter to complete.

```
```text
[student@TargetFedora01 ~]$ su -c 'useradd dbadmin1'
Password:
[student@TargetFedora01 ~]$ su -c 'passwd dbadmin1'
Password:
Changing password for user dbadmin1.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```
```

**Figure 15 – Adding user account and setting password**

+   17.  Force a password change for each user the first time they login.
+       a)  Type the command: `su -c 'chage -d 0 dbadmin1'` and press <enter>.
+       b)  Password: ISS316$Security
+       c)  Type the command: `su -c 'chage -d 0 dbadmin2'` and press <enter>.
+       d)  Password: ISS316$Security
+       e)  Type the command: `su -c 'chage -d 0 webadmin1'` and press <enter>.
+       f)  Password: ISS316$Security
+       g)  Type the command: `su -c 'chage -d 0 webadmin2'` and press
+       h)  Password: ISS316$Security

**Note :** After the `-d`, it should be a zero, not the letter `o`.

+   18.  Create two group accounts one named `dba` and another named `web`.
+       a)  Type the command: `su -c 'groupadd dba'` and press <enter>.
+       b)  Password: ISS316$Security
+       c)  Type the command: `su -c 'groupadd web'` and press <enter>.