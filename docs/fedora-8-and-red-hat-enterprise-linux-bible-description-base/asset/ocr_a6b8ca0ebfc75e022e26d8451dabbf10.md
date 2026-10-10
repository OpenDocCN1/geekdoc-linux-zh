# User-level security

When you create a shared volume (in AppleVolumes.default), you can indicate which users can access that volume. Users can be authenticated using clear-text passwords (to log in to their basic Linux user accounts) or by setting up a special encrypted password file using netatalk.

Users can be assigned to particular volumes when they define those volumes in the AppleVolumes.default file as described earlier. Here’s an example where the users mike and jojo and anyone in the group wheel are allowed access to a volume:

```
/var/homework "History homework" allow:mike,jojo,@wheel
```

To use the default clear-text passwords, you need only set up user accounts as you normally would in Linux (see Chapter 11). However, to use encrypted passwords for users (on a server configured to use encrypted passwords in the afpd.conf file as described earlier), you must create an AppleTalk password file (/etc/atalK/afppasswd). As root, type the following:

```
# afppasswd -c
```

This command gathers all regular users (UID 100 and above) and the guest user (nobody) and adds them to the afppasswd file.

Next, you need to add proper passwords for each of the users just added to the afppasswd file that will be allowed access to your netatalk shares. For example:

```
# afppasswd jake
Enter NEW AFP password: ********
Enter NEW AFP password again: ********
```

After you create afppasswd initially, you can later add individual users manually to that file (provided they also have valid Linux accounts). Do that using -a option to afppasswd:

```
# afppasswd -a cindy
Enter NEW AFP password: ********
Enter NEW AFP password again: ********
```

Issues related to choosing a good password (see Chapter 14) are true for setting AppleTalk passwords as well. If the passwords match, the user will be able to log in using the assigned user name and password when he tries to mount the AppleTalk volume from the netatalk server, provided the netatalk service is using encrypted authentication (uams_dxh.so).

# Host-level security

You can restrict which computers on your network have access to your netatalk services using the /etc/hosts.allow and /etc/hosts.deny files. These files are described in the “Using TCP wrappers” section of Chapter 14. These are the same files you use to allow or restrict access to other Linux networking services.