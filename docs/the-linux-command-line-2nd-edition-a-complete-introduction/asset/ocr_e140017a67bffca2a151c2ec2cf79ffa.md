we now see that, in fact, our three functions are being executed.

With our function framework in place and working, it’s time to flesh out some of the function code. First, the report_uptime function:

```
report_uptime () {
    cat <<-_EOF_
        <H2>System Uptime</H2>
        <PRE>$(uptime)</PRE>
    _EOF_
    return
}
```

It’s pretty straightforward. We use a here document to output a section header and the output of the uptime command, surrounded by <PRE> tags to preserve the formatting of the command. The report_disk_space function is similar:

```
report_disk_space () {
    cat <<-_EOF_
        <H2>Disk Space Utilization</H2>
        <PRE>$(df -h)</PRE>
    _EOF_
    return
}
```

This function uses the df -h command to determine the amount of disk space. Lastly, we’ll build the report_home_space function:

```
report_home_space () {
    cat <<-_EOF_
        <H2>Home Space Utilization</H2>
        <PRE>$(du -sh /home/*)</PRE>
    _EOF_
    return
}
```

We use the du command with the -sh options to perform this task. This, however, is not a complete solution to the problem. While it will work on some systems (Ubuntu, for example), it will not work on others. The reason is that many systems set the permissions of home directories to prevent them from being world-readable, which is a reasonable security measure. On these systems, the report_home_space function, as written, will