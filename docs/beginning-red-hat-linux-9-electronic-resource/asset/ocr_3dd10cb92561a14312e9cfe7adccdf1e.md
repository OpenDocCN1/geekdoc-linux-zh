```
$ passwd
Changing password for user eziodm.
Changing password for eziodm
(current) UNIX password: (password not shown)
```

Then you're asked to enter the new password. We can take this opportunity to find out the sort of passwords that are acceptable. Try typing `ape5` as your new password:

```
New password: (password not shown)
BAD PASSWORD: it is too short
```

Since `ape5` is too short, try `elephant6` instead:

```
New password: (password not shown)
BAD PASSWORD: it is based on a dictionary word
```

The `passwd` command won't accept dictionary-based passwords either; it has an inbuilt mechanism that prevents you from choosing passwords that can be easily guessed. Try something a little more complex, like `e!eph4nt`:

```
New password: (password not shown)
Retype new password: (password not shown)
passwd: all authentication tokens updated successfully.
```

As you can see, the steps in the command line procedure are identical to those of the GUI-based procedure.

> Finally, remember that if a normal user, like eziodm, forgets their password, root can run the following command to reset it to a known value:

```
# passwd eziodm
```

# Changing Your Own Account Description and Shell

Red Hat Linux also provides GUI and CLI utilities that allow a user to control other aspects of their account. You can launch the GUI utility by selecting **Main Menu | Preferences | About Myself** or by typing `userinfo` at the command line. This will bring up the User Information dialog: