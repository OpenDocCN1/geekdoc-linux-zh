# Deleting a Group

You must specify the name of the group to be created, *group*. If you do not specify a group ID, the next group ID will be used. If you want to create a system group—one with a group ID less than 500—specify -r as an argument before the group name. See the man page for groupadd for additional information.

To delete a group via the command line, issue the groupdel command, which has the following form:

```
groupdel group
```

See the man page for groupdel for additional information.

# Modifying Group Name

To modify the name of a group via the command line, issue the groupmod command, which has the following form:

```
groupmod -n newewame group
```

See the man page for groupmod for additional information.

# Modifying Group Membership

To modify membership of a group via the command line, you must manually edit /etc/group or issue the usermod command to adjust the group membership of each affected user. Generally, this means you must issue the command several times; thus, it's often more convenient to modify group membership via userconf from the command line. The usermod command is described earlier in this chapter.