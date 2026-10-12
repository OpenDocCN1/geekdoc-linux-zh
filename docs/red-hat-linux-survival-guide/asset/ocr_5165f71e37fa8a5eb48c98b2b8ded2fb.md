# Changing the home directory

To change the home directory of an existing user, run the usermod command as follows, where new_home_directory and username are the correct values:

```
usermod -d new_home_directory username
```

For example, if a user called keller has /home/keller as her home directory, and you want to move it to /home2/keller, you would run the usermod command as follows:

```
usermod -d /home2/keller keller
```

This sets the new directory as keller’s home directory. If you want to move the contents of a user’s existing home directory to the new location, use the -m option. For user keller, the command would be as follows:

```
usermod -d -m /home2/keller keller
```

# Changing a UID

To change the UID of a user, run the usermod command as follows, where UID and username are the correct values:

```
usermod -u UID username
```

For example, the following command changes the UID for user mrfrog to 500:

```
usermod -g 500 mrfrog
```

All the files and directories owned by the user within mrfrog’s home directory will automatically reflect the UID change. However, if the user owns files outside her own home directory, you will have to manually change the ownership using the chown command.

# Changing a default group

To change a user’s default group, run the usermod command as follows, where group_name_or_GID and username are the correct values:

```
usermod -g group_name_or_GID username
```