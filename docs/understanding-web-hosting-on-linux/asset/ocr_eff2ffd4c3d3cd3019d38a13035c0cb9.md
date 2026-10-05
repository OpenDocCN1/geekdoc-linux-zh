* /var/log/secure

# ## Exercise 4: Perform Routine Maintenance

+   1. Using Webmin, click the System tab, then click Scheduled Cron Jobs.
2. Click the Logrotate link to determine when the logrotate command is executed.
3. Back up, using the `tar` utility:

```
# tar -cjf mybackup.tbz /etc /var/www /home /usr/local
```

+   a) Explain why the .tbz extension is used.
b) What does each of the cjf options do?