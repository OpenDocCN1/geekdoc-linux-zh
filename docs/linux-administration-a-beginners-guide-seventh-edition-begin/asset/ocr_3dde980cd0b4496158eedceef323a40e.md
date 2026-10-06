# CHAPTER 5 Managing Users and Groups 149

6. Create the final user account, called bogus. But this time, specify the user’s shell to be the tcsh shell, and let the user’s default primary group be the system “games” group:

```
[root@server ~]# useradd -s /bin/tcsh -g games bogus
```

7. Examine the /etc/passwd file for the entry for the bogususer:

```
[root@server~]# grep bogususer /etc/passwd
bogususer:x:1003:/home/bogususer:/bin/tcsh
```

From this, you can tell the following:

+   * The UID is 1003.
* The G is 20.
* A home directory is also created for the user under the /home directory.
* The user’s shell is /bin/tcsh.

# Creating Groups with groupadd

Next, create a couple of groups, nonsystem and system.

+   1. Create a new group called research:

```
[root@server ~]# groupadd research
```

+   2. Examine the entry for the research group in the /etc/group file:

```
[root@server ~]# grep research /etc/group
research:x:1002:
```

This output shows that the group ID for the research group is 1002.

+   3. Create another group called sales:

```
[root@server ~]# groupadd sales
```

+   4. Create the final group called bogus, and force this group to be a system group (that is, the GID will be lower than 999). Type the following:

```
[root@server ~]# groupadd -r bogus
```

+   5. Examine the entry for the bogus group in the /etc/group file:

```
[root@server ~]# grep bogus /etc/group
bogus:x:988:
```

The output shows that the group ID for the bogus group is 988.