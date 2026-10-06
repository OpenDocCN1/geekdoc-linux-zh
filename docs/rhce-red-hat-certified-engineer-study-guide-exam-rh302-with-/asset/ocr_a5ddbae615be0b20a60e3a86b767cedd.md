# 382  Chapter 16 • Using the cron System

In response to the crontab -e command, the cron system will launch the default system editor. If you prefer to use a different editor, you can set the environment variable EDITOR before issuing the crontab command. For example,

```
export EDITOR=/usr/bin/pico
crontab -e
```

lets the user edit the crontab by using the pico editor. 
A user can remove the user's crontab entirely, by issuing the command

```
crontab -r
```

The root user can remove a user's crontab by issuing a command of the form

```
crontab -u user -r
```

where user is the login name of the user whose crontab is to be removed. 
The crontab entries are specified as specially formatted lines; the next subsection explains the format in which they may appear.

# Format of the crontab File

The crontab file may contain these sorts of lines:

+   - Comment lines
- Environment settings
- cron commands

Within a line, leading spaces and tabs are ignored. Blank lines and lines beginning with a hash mark (#) are considered comment lines and are ignored by the cron system.

# Specifying Environment Settings

Environment settings lines have the form

```
name = value
```

Such lines specify environment variable names and associated values. A cron job can access these environment variables. The following environment variables are available without explicit definition:

+   - SHELL is bound to /bin/sh
- LOGNAME is bound to the user's login name