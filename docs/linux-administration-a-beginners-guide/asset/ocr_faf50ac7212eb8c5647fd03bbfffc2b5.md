| Options | Descriptions |
|---|---|
| -g gid | Specifies the GID for the new group as gid. By default, this value is automatically chosen by finding the first available value. |
| -r | By default, Red Hat searches for the first GID that is higher than 499. The -r options tell groupadd that the group being added is a system group and should have the first available GID under 499. |
| -f | When adding a new group, Red Hat Linux will exit without an error if the specified group to add already exists. By using this option, the program will not change the group setting before exiting. This is useful in scripting cases where you want the script to continue if the group already exists. |
| group | This option is required. It specifies the name of the group you want to add to be group. |

# Table 5-2. More Command Options and Their Descriptions

# groupdel

Even more straightforward than userdel, the groupdel command removes existing groups specified in the /etc/group file. The only usage information needed for this command is this:

```
groupdel group
```

where group is the name of the group to remove. For example, if you wanted to remove the research group, you would issue this command:

```
[root@ford /root]# groupdel research
```

# groupmod

The groupmod command allows you to modify the parameters of an existing group. The options for this command are

```
groupmod -g gid -n group-name group
```

where the -g option allows you to change the GID of the group, the -n options allows you to specify a new name of a group, and of course you need to specify the name of the existing group as the last parameter.

For example, if the superman research group wanted to change its name to batman, you would issue the command: