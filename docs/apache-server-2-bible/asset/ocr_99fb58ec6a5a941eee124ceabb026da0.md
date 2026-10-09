![](bbox=[0.13, 0.12, 0.18, 0.18])

Setting the -auto option ensures that user is removed from all the groups in the group table.

# ### Updating an existing user’s password in the user table

To update a user's password in the user table, run the following command:

```
manage_user.pl -db=user \
-action=update \
-user=user_name \
-dbpwd=database_password
```

For example, to update user kabi r's password to mydbpwd by using the mydbpwd database password, run the following command:

```
manage_user.pl -db=user \
-action=update \
-user=kabir \
-dbpwd=mydbpwd
```

# ### Adding a user to a group

To add an existing user to a new or existing group, run the following command:

```
manage_user.pl -db=group \
-action=add \
-user=user_name \
-group=group_name \
-dbpwd=database_password
```

For example, to add a user named kabir to a group called administrators, run the following command:

```
manage_user.pl -db=group \
-action=add \
-user=kabir \
-group=administrators \
-dbpwd=mydbpwd
```

Here mydbpwd is the database password needed to write to group table.

# ### Deleting a user from a group

To delete a user from a group, run the following command :

```
manage_user.pl -db=group \
-action=del \
-user=user_name \
-group=group_name \
-dbpwd=database_password
```