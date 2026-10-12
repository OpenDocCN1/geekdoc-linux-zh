# Adding New Users

The command-line approach to adding this user is actually quite simple and can be accomplished on a single line. In the example shown here, the sysadmin uses the `useradd` command to add the new user `bernice`. The command `adduser` (a variant found on some UNIX systems) is a symbolic link to `useradd`, so both commands work the same. In this example, we use the `-p` option to set the password the user requested; we use the `-s` option to set his special shell, and the `-u` option to specify his UID. (If we created a user with the default settings, we would not need to use these options.) All we want to do can be accomplished on one line:

```
# useradd bernice -p sJt1ch3r -s /bin/zsh -u 507
```

The sysadmin can also use the graphical interface that Fedora provides, as shown in Figure 14.2. It is accessed as the Users and Groups item from the Administration menu item. Here, the sysadmin is adding a new user to the system where user bernice uses the bash command shell.

![](bbox=[0.18, 0.43, 0.85, 0.76])

**FIGURE 14.2** Adding a new user is simple. The GUI provides a more complete set of commands for user management than for group management.

These are the steps we used to add the same account as shown in the preceding command, but using the graphical User Manager graphical interface:

+   1.  Launch the Fedora User Manager graphical interface by clicking on the Users and Groups menu item found in the System Settings menu.