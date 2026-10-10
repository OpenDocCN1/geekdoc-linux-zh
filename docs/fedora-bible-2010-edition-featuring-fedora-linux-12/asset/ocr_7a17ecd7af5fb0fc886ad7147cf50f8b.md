```
Changing password for user jsmith.
New password: ******
Retype new password: ******
```

The `passwd` command will let you know if it thinks you selected a bad password, one that could be easily guessed by using a dictionary or is too short or too simple.

**CROSS-REFERENCE:** See Chapter 14 for tips on creating good passwords.

In creating the account for John, the `useradd` command performs several actions:

+   · Reads the `/etc/login.defs` and `/etc/default/useradd` files to get default values to use when creating accounts.
+   · Checks command-line parameters to find out which default values to override.
+   · Creates a new user entry in the `/etc/passwd` and `/etc/shadow` files based on the default values and command-line parameters.
+   · Creates any new group entries in the `/etc/group` file.
+   · Creates a home directory based on the user's name and places it in the `/home` directory.
+   · Copies any files located within the `/etc/skel` directory to the new home directory. This usually includes login and application startup scripts.

The preceding example uses only two of the available `useradd` options. Most account settings are assigned using default values. Here's an example that uses a few more options:

```
# useradd -m -g users -G wheel,sales -s /bin/tcsh -c "Mary Smith" mary
```

In this case, the `useradd` command is told to create a home directory for the user `mary` (-m), make `users` the primary group she belongs to (-g), add her to the groups `wheel` and `sales` (-G), and assign `tcsh` as her primary command shell (-s). Note that the `wheel` and `sales` groups must already exist for this example to work. This results in a line similar to the following being added to the `/etc/passwd` file:

```
mary:x:502:100:Mary Smith:/home/mary:/bin/tcsh
```

In the `/etc/passwd` file, each line represents a single user account record. Each field is separated from the next by a colon (:) character. The field's position in the sequence going left to right determines what it is. As you can see, the login name is first. The password field contains an x because Fedora is using a shadow password file in which to store encrypted password data. The user ID selected by the `useradd` command is 502. The primary group ID is 100, which corresponds to the `users` group in the `/etc/group` file. The comment field was correctly set to Mary Smith, the home directory was automatically assigned as `/home/mary`, and the command shell was assigned as `/bin/tcsh`, exactly as specified with the `useradd` options.

If you omit many of the options (as I did in the first `useradd` example), defaults are assigned in most cases. For example, if you didn't use `-g users` or `-G wheel,sales`, a group named