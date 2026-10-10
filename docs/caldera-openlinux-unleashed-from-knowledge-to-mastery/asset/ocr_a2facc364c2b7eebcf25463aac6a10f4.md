# # Example 1: A Superuser

Suppose you want to create a user, `slackhacker`, who will have root privileges—access to everything. `slackhacker` will be able to connect to the server from any host and wants to use `topsecret` as his/her password.

To do this by direct modification, enter the following commands:

```
```
mysql> INSERT INTO user values('localhost','slackhacker'
   ->,PASSWORD(' topsecret'),'Y','Y','Y','Y','Y','Y','Y','Y'
   ->'Y','Y','Y','Y','Y','Y');
mysql> INSERT INTO user VALUES('%','slackhacker',PASSWORD('topsecret')
   -> ,'Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y');
```
```

When you are doing direct modification, you must also tell the server to reload the tables:

```
```
mysql> FLUSH PRIVILEGES;
```
```

> **Caution**
> 
> Note that you enter the password inside the `PASSWORD` function. This function encodes the password to an unreadable form so other users can't see your password by just entering:
> 
> ```sql
> mysql> SELECT * FROM user WHERE(user='slackhacker');
> ```
> 
> You definitely don't want that, do you? So be sure you use the `PASSWORD` function.

> **Note**
> 
> Note that you have to type a semicolon (;) to end a command.

You probably wonder why we entered two separate rows for both `slackhacker@localhost` and `slackhacker@%` (which means `slackhacker` at any host). If we don't do this, the anonymous user entry for `localhost`, created by `mysql_install_db`, will be used instead. The reason is that the anonymous user entry has a more specific `Host` field value and therefore it comes earlier in the user table sort order. For more information on this, read the MySQL documentation, which can be found at `www.mysql.com`.