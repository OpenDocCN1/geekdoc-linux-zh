# PUTTING A COMMAND INTO THE BACKGROUND: &

Making a command run in the background is simple; you simply add an & to the end of the line containing the command.

For example, suppose you are running a program called analog to analyze your Web server logfiles. Most log analysis takes quite some time for a busy Web server, so you probably don't want to wait around for the command to finish. In order to run analog in the background, you can just type the following:

```
>analog /var/log/httpd/access_log &
[3] 32566
>
```

The results are a bit cryptic, but you can see that you are returned to the command line, ready to go about your business! The two numbers that are returned identify the process on the system. The first result, [3], identifies this as process number 3 that you've sent to the background. The second number, 32566, is the process ID. Your UNIX system potentially has hundreds of processes running on it, and each one is assigned a unique number. Whatever number your process happens to be assigned is returned as the second result value.

![](bbox=[0.1, 0.82, 0.15, 0.9])

> Running More than One Command To run several commands, one after the other, and put the whole group into the background, you can use the following syntax: {<command 1>; <command 2>; < command 3>} &. This creates a new shell to execute the commands and places it in the background. For example, if you wanted to run the analog utility on two files, you might use something such as the following: (analog /var/log/httpd/access_log; analog /var/log/httpd/new_access_log) &