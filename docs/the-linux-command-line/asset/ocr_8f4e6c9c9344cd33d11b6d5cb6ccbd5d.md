```
<TITLE>System Information Report For twin2</TITLE>
<HEAD>
<BODY>
<H1>System Information Report For linuxbox</H1>
<P>Generated 03/19/2009 04:02:10 PM EDT, by me</P>

</BODY>
</HTML>
```

we see that there are some blank lines in our output after the time stamp, but we can’t be sure of the cause. If we change the functions to include some feedback:

```
report_uptime () {
    echo "Function report_uptime executed."
    return
}

report_disk_space () {
    echo "Function report_disk_space executed."
    return
}

report_home_space () {
    echo "Function report_home_space executed."
    return
}
```

and run the script again:

```
[me@linuxbox ~]$ sys_info_page
<HTML>
<HEAD>
<TITLE>System Information Report For linuxbox</TITLE>
</HEAD>
<BODY>
<H1>System Information Report For linuxbox</H1>
<P>Generated 03/20/2009 05:17:26 AM EDT, by me</P>
Function report_uptime executed.
Function report_disk_space executed.
Function report_home_space executed.
</BODY>
</HTML>
```