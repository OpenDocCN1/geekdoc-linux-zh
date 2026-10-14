The backslash (\ ) enables you to write a single long command on several lines.

While in mailx, you can see what aliases are defined by using the alias command without arguments. You can also define temporary aliases at the mailx prompt that are in effect during that mailx session.

# 11.6.2 Setting Mail Variables

Mail variables are similar to variables in your .login file. They can be binary, string, or numeric.

To set a binary mail variable in your .mailrc file, enter the set command followed by the option name. The sample .mailrc file includes these binary variables:

```
set ask
set askcc
unset dot
```

+   - Setting ask makes mailx prompt you for the subject line of messages you send.
+   - Setting askcc makes mailx prompt you for carbon-copy recipients.
+   - Unsetting dot makes mailx refuse to end a message when you type a line with just a period on it; you would have to end a message by pressing Ctrl/D instead.

String mail variables accept characters or numbers as values. The sample .mailrc file includes the following three string variables:

```
set folder=folder
set record=/usr/users/hale/folder/outgoing
set crt=20
```