```
stat --format="Size: %s bytes" --printf="%h\n" filename
```

`%h` in `--printf` provides human-readable file size.

# 88. watch: Execute a command repeatedly and display the results.

The `watch` command in Linux is a handy utility that allows you to execute a given command periodically and display the results in real-time. This can be particularly useful for monitoring changes or updates in the output of a command without having to rerun it manually each time.

Examples:

1. Simple Usage:

```
watch date
```

This will continuously update and display the current date and time every 2 seconds (by default).

2. Monitor Disk Space:

```
watch df -h
```