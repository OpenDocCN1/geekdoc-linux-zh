+   6. **Display the logins for a specific period:**

```
last -s YYYY-MM-DD -t YYYY-MM-DD
```

Replace the start date ( `-s` ) and end date ( `-t` ) with the desired date range. This command will show logins within the specified period.

+   7. **Display IP addresses along with user logins:**

```
last -i
```

This option includes IP addresses along with user logins, providing additional information about the origin of the logins.

+   8. **Display hostname in the output:**

```
last -a
```

The `-a` option shows the hostname in the output, providing information about which host the user logged in from.

83. stty: Change and print terminal line settings.