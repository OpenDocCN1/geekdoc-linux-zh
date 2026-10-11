your environment by setting the USER variable. For example, you can use the following set command to specify a username of sampa dm:

```
C:\> set USER=sampadm
```

If you set the USER environment variable by using the System item in the Control Panel, it takes effect for each console window and you won't have to issue it at the prompt.

+   -p (alternative form: --password)

This option tells mysql to ask you for your MySQL password by displaying an Enter password: prompt. For example:

```
mysql -h host_name -p -u user_name
Enter password:
```

When you see the Enter password: prompt, type in your password. (The password won't be echoed to the screen, in case someone's looking over your shoulder.) Note that your MySQL password is not necessarily the same as the password that you use to log in to Unix or Windows.

If you omit the -p option, mysql assumes that you don't need one and doesn't prompt for it.

Another way to specify this option is to indicate the password value directly on the command line by typing the option as -p*your_pass* (alternative form: --password= your_pass). However, for security reasons, it's best not to do that. The password becomes visible to others that way.

If you do decide to specify the password on the command line, note particularly that there is no space between the -p option and the following password value. This behavior of -p is a common point of confusion, because it differs from the -h and -u options, which are associated with the word that follows them regardless of whether there is a space between the option and the word.

Suppose that your MySQL username and password are sampadm and secret. If the MySQL server is running on the same host where you are going to run mysql, you can leave out the -h option and the mysql command to connect to the server. It looks like this:

```
% mysql -p -u sampadm
Enter password: ******
```

After you enter the command, mysql prints Enter password: to prompt for your password, and you type it in (the ****** indicates where you type secret).

If all goes well, mysql prints a greeting and a mysql> prompt indicating that it is waiting for you to issue queries. The full startup sequence looks something like this:

```
% mysql -p -u sampadm
Enter password: ******
Welcome to the MySQL monitor. Commands end with ; or \g.
```