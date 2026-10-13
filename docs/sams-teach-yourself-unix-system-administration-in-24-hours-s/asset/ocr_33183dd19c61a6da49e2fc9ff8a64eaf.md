# Using Groups to Control Access

As a demonstration of how to work with groups in Unix, let's control access to the printer on this system. We're going to change permissions on the printing application to only allow access to members of the lp group. To do this, we're going to add a password to the lp group, then change the permissions of the lp binary to match.

# Task 4.4: Access Control with Groups

Using groups to control access to the lp command proves an informative and illustrative example. I should let you know up front that a more common solution to this problem is to rename the lp command something like lp.authorized, then create a shell script called lp1 that checks user ID against a list of valid, authorized users.

The downside of the authorization list, of course, is that it must be maintained. Creating an lp group is more elegant in many ways because the administrator needs simply to give out the password and a user is authorized. If you want to disable a single user, however, it's a bit of a problem.

+   1. The first step is to make sure that there's an lp group in the /etc/group file. Easily done with grep, fortunately:
+   
+      ```
+      # grep lp /etc/group
+      lp:x:7:daemon,lp
+      ```
+   
+      Looks good. Now let's add user mdella to the list to ensure that he can print whenever he wants without fuss. This can be done in a variety of ways, but the group editing utility vigr is really the optimal solution. So, that'll let me change the line above (in the non-shadow groups file) to
+   
+      ```
+      # grep lp /etc/group
+      lp:x:7:daemon,lp,mdella
+      ```
+   
+   2. Setting the password for a group can be a very hard task on most Unix systems. Linux has the helpful gpasswd program that enables you to specify the password for a group, but most Unices have no equivalent. As a result you are left changing the password of a regular user account, then copying-and-pasting the encrypted password string into the group file. Ugh.
+   
+      Making this even more complex, modern Unices use a shadow password file, meaning that the passwords themselves (encrypted) are kept in a different file than the account information. With the group file, passwords are stored in /etc/gshadow. By default, the lp group password is left blank (unmatchable):
+   
+      ```
+      # grep lp /etc/gshadow
+      lp::daemon,lp
+      ```