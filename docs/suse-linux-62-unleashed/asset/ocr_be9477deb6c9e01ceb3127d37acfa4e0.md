# Networking and Internet Services
PART II

The field for the user's home directory is broken up by the ./ / characters. The effective root directory is listed before the split characters, and the user's relative home directory is listed after the split characters. For example, consider the following password entry:

```
user1:encrypted password:500:128:User 1:/home/ftp/:user1:/bin/false
```

Here, /home/ftp is the user's new relative root directory (the bin, etc, tcp, pub, and lib directories are under the /home/ftp by default, and /home/ftp/user is the user's home directory). Note that the false command is used when user logs in; although the ftppass page documents the use of ftpponly, this command will not be found with Linux—use of false is considered an acceptable substitute. (Don't forget to put /bin/false in your system's /etc/shells file.)

# limit

The limit command enables you to control the number of users by class and time of day. This is especially useful if you have a popular archive but the system needs to be available to your users during business hours. The format of the limit command follows:

```
limit <class> <n> <times> <message_file>
```

<class>is the class to limit, <n> is the maximum number of people allowed in that class, <times> is the time during which the limit is in effect, and <message_file> is the file that will be displayed to the client when the maximum limit is reached.

The format of the <times> parameter is somewhat complex. The parameter is in the form of a comma-delimited string, where each option is for a day. The days Monday through Saturday take the Su, Mo, Tu, We, Th, and Sa, respectively, and all the weekdays can be referenced as Wk. Time should be kept in military format without a colon separating the hours and minutes. A range is specified by the dash character.

For example, you would use the following limit line to limit the class nonanonks to 10 users from Monday through Thursday, all day, and Friday from midnight to 5 p.m.:

```
limit nonanonks 10 MoTuThFr0000-1700 /home/ftp/.message.to_many
```

If the limit is reached in this case, the contents of the file /home/ftp/.message.to_many are displayed to the connecting user.

# loginfails

The loginfails command enables you to disconnect clients after they've reached their predetermined number of failed login attempts. By default, this is five; however, you can set it by using the following command:

```
loginfails <n>
```