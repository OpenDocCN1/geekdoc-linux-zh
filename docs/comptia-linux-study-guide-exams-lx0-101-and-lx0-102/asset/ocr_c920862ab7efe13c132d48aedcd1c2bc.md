# Chapter 9 • Writing Scripts, Configuring Email, and Using Databases

```
$ env | grep HOSTNAME
HOSTNAME=carson.example.com
```

Of course, the variables you see and their values will be unique to your system and even yourour account—that's the whole point of environment variables. Table 9.1 summarizes com-
mon variables you may see in this output.

# TABLE 9.1 Common environment variables and their meanings

| Variable name | Explanation |
|---|---|
| USER or USERNAME | This is your current username. It's a variable's maintained by the system. |
| SHELL | This variable holds the path to the current command shell. |
| PWD | This is the present working directory. This environment variable is maintained by the system. Programs may use it to search for files when you don't provide a complete path. |
| HOSTNAME | This is the current TCP/IP hostname of the computer. |
| PATH | This is an unusual important environment variable. It sets the path for a session, which is a colon-delimited list of directories in Linux servers for executable programs when you type a program name. For instance, if PATH is /bin:/usr/bin and you type ls, Linux looks for an executable program called ls in /bin/bin and then in /usr/bin. If the command you isn't on the path, Linux responds with a command not found. The PATH variable is typically built up in several configuration files, as /etc/profile and the .bashrc file in the user home directory. |
| HOME | This variable points to your home directory. Some programs use it to help them look for configuration files or a default location in which to store files. |
| MAIL | This variable holds the location of the user's mail pool. It's usually /var/spool/mail/username. |
| LANG | The system holds your current language, specified as a locale, using this variable. Locales are described further in Chapter 6, "Config the X Window System, Localization, and Printing." |
| TZ | You can set this environment variable to your own time zone, which is most useful if that's different than the computer's time zone--for instance, if you're using a computer remotely. Chapter 6 describes the formats you can use when setting the time zone in this way. |