
And then we run the script again:

```
```text
[me@linuxbox ~]$ sys_info_page
<HTML>
        <HEAD>
                <TITLE>System Information Report For linuxbox</TITLE>
        </HEAD>
        <BODY>
                <H1>System Information Report For linuxbox</H1>
                <P>Generated 03/20/2012 05:17:26 AM EDT, by me</P>
                Function report_uptime executed.
                Function report_disk_space executed.
                Function report_home_space executed.
        </BODY>
</HTML>
```
```

We now see that, in fact, our three functions are being executed. With our function framework in place and working, it’s time to flesh out some of the function code. First, the report_uptime function:

```
```bash
report_uptime () {
        cat <<- _EOF_
                <H2>System Uptime</H2>
                <PRE>$(uptime)</PRE>
                _EOF_
        return
}
```
```

It’s pretty straightforward. We use a here document to output a section header and the output of the uptime command, surrounded by `<PRE>` tags to preserve the formatting of the command. The report_disk_space function is similar:

```
```bash
report_disk_space () {
        cat <<- _EOF_
                <H2>Disk Space Utilization</H2>
                <PRE>$(df -h)</PRE>
                _EOF_
        return
}
```
```

This function uses the `df -h` command to determine the amount of disk space. Lastly, we’ll build the report_home_space function:

```
```bash
report_home_space () {
        cat <<- _EOF_
                <H2>Home Space Utilization</H2>
                <PRE>$(du -sh /home/*)</PRE>
                _EOF_
        return
}
```
```

We use the du command with the -sh options to perform this task. This, however, is not a complete solution to the problem. While it will work on some systems (Ubuntu, for example), it will not work on others. The reason is that many systems set the permissions of home directories to prevent them from being world readable, which is a reasonable security measure. On these systems, the report_home_space function, as written, will work only if our script is run with superuser privileges. A better solution would be to have the script adjust its behavior according to the privileges of the user. We will take this up in Chapter 27.

## SHELL FUNCTIONS IN YOUR .BASHRC FILE

Shell functions make excellent replacements for aliases, and they are actually the preferred method of creating small commands for personal use. Aliases are very limited in the kind of commands and shell features they support, whereas shell functions allow anything that can be scripted. For example, if we liked the report_disk_space shell function that we developed for our script, we could create a similar function named ds for our .bashrc file:

```
ds () {
    echo "Disk Space Utilization For $HOSTNAME"
    df -h
}
```

## Final Note

In this chapter, we have introduced a common method of program design called top-down design, and we have seen how shell functions are used to build the stepwise refinement that it requires. We have also seen how local variables can be used to make shell functions independent from one another and from the program in which they are placed. This makes it possible for shell functions to be written in a portable manner and to be reusable by allowing them to be placed in multiple programs—a great time saver.

## 27

## FLOW CONTROL: BRANCHING WITH IF

In the last chapter, we were presented with a problem. How can we make our report-generator script adapt to the privileges of the user running the script? The solution to this problem will require us to find a way to “change directions” within our script, based on the results of a test. In programming terms, we need the program to branch.

Let’s consider a simple example of logic expressed in pseudocode, a simulation of a computer language intended for human consumption:

```
X = 5
If X = 5, then:
    Say "X equals 5."
Otherwise:
    Say "X is not equal to 5."
```
