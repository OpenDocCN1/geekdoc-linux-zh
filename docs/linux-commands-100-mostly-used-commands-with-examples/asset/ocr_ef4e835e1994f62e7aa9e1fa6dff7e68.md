This command will periodically display the disk space usage, updating every 2 seconds by default.

# 3. **Check System Resource Usage:**

```
watch -n 1 top
```

The `-n` option allows you to specify the update interval in seconds. In this example, `top` will be refreshed every 1 second, providing real-time information about system resource usage.

# 4. **Monitor Log Files:**

```
watch -n 5 tail /var/log/syslog
```

This example watches the system log file, updating every 5 seconds. It can be useful for keeping an eye on log entries as they occur.

# 5. **Track File Changes:**

```
watch -d ls -l
```

The `-d` option highlights the differences between successive updates. In this case, it shows changes in the file listing with each refresh.