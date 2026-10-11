# ## Modifying User Accounts

To modify the information regarding a user account after creation, you can edit the /etc/passwd or /etc/shadow file; however, this is not recommended practice because typographical errors in these files might prevent the system from functioning. The **usermod command** can be used to modify most information regarding user accounts. For example, to change the login name of the user bobj to barb, you can use the -l option to the usermod command:

```
```
[root@server1 root]# usermod -l barb bobg
[root@server1 root]# _
```
```

Table 11-7 displays a complete list of options used with the usermod command to modify user accounts.

**Table 11-7 Common options to the usermod command**

| Option | Description |
| :--- | :--- |
| -c "description" | Specifies a new description for the user in the GECOS field of /etc/passwd |
| -d homedirectory | Specifies the absolute pathname to a new home directory |
| -e expirydate | Specifies a date to disable the account from logging in |
| -f days | Specifies the number of days until a user account with an expired password is disabled |
| -g group | Specifies a new primary group for the user account |
| -G group1, group2, etc. | Specifies all other group memberships for the user account |
| -l name | Specifies a new login name |
| -s shell | Specifies the absolute pathname to a new shell used for the user account |
| -u UID | Specifies a new UID for the user account |