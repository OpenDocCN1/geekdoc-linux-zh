you can create or modify groups by directly editing the configuration files in question. Their layout is similar to that for account control files, but the details differ.

# # Adding Groups

Linux provides the groupadd command to add a new group. This utility is similar to useradd but has fewer options. The groupadd syntax is as follows:

```
groupadd [-g GID [-o]] [-r] [-f] groupname
```

The parameters to this command enable you to adjust its operation:

+   * Specify a GID You can provide a specific GID with the -g GID parameter. If you omit this parameter, groupadd uses the next available GID. Normally, the GID you specify must be unused by other groups, but the -o parameter overrides this behavior, allowing you to create multiple groups that share one GID.

+   * Create a sub-500 GID The -r parameter instructs groupadd to create a group with a GID of less than 500. Not all distributions support this option; it was added by Red Hat and has been used on some related distributions. Red Hat uses GIDs of 500 and above for user private groups (that is, groups named after individual users), hence the -r parameter.

+   * Force creation Normally, if you try to create a group that already exists, groupadd returns an error message. The -f parameter suppresses that error message. Not all versions of groupadd support this parameter.

In most cases, you'll create groups without specifying any parameters except for the group name itself:

```
# groupadd project3
```

This command creates the project3 group, giving it whatever GID the system finds convenient—usually the highest existing GID plus 1. Once you've done this, you can add users to the group, as described in the next section. When you add new users, you can add them directly to the new group with the -g and -G parameters to useradd, described earlier.

# # Modifying Group Information

Group information, like user account information, may be modified either using utility programs or by directly editing the underlying configuration file, /etc/group. There are fewer options for modifying groups than for modifying accounts, and the utilities and configuration files are similar. In fact, usermod is one of the tools that's used to modify groups.

# ## Using groupmod and usermod

The groupmod command modifies an existing group's settings. Its syntax is as follows:

```
groupmod [-g GID [-o]] [-n newgroupname] oldgroupname
```