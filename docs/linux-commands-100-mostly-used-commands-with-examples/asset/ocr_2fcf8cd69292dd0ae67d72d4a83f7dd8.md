```
man locate
```

Displays the manual page for the `locate` command, providing detailed information on its usage and options.

# 82. last: Show a listing of last logged in users.

The `last` command in Linux is used to display information about the last logged-in users on the system. It extracts data from the `/var/log/wtmp` file, which keeps track of login and logout activity.

Examples:

+   1. **Display the last logged-in users:**

```
last
```

This will display a list of users who have logged in, along with their login and logout times, as well as the duration of their sessions.

+   2. **Display the last 5 logins:**

```
last -n 5
```