# Apply Your Knowledge

# Exercises

# 20.1 Creating a User and a Role

Estimated Time: 20 minutes

To create a user and a role, perform the following steps:

+   1. Create the role named admin1, as shown here:
```
roleadd -u 2000 -g 10 -d /export/home/
admin1 -m admin1
passwd admin1
<assign a password to the role account>
```
2. Create a profile to allow the user to shut down a system.
Edit the /etc/security/prof_attr file and enter the following line:
```
Shutdown:::Permit system shutdown:
```
Save and exit the file.
3. Add the Shutdown and All profiles to the role as follows:
```
rolemod -P Shutdown,All admin1
```
4. Verify that the changes have been made to the user_attr database:
```
more /etc/user_attr
```
5. Create the user account and assign it access to the admin1 role:
```
useradd -u 3000 -g 10 -d /export/home/
trng1 -m -s /bin/ksh -R admin1 trng1
```

+   6. Assign a password to the new user account as follows:
```
passwd trng1
<assign a password>
```
7. Verify that the entry has been made to the passwd, shadow, and user_attr files as follows:
```
more /etc/passwd
more /etc/shadow
more /etc/user_attr
```
8. Assign commands to the Shutdown profile:
Edit the /etc/security/exec_attr file and add the following line:
```
Shutdown:suser:cmd::/usr/sbin/shutdown:uid=0
```
Save and exit the file.
9. Test the new role and user account as follows:
a. Log in as trng1.
b. List the profiles that are granted to you by typing the following:
```
roles
```
c. Use the su command to assume the role admin1:
```
su admin1
<enter the password for admin1>
```
d. List the profiles that are granted to you by typing the following:
```
profiles
```
e. Shut down the system:
```
/usr/sbin/shutdown -i 0 -g 0
```