```
% /usr/lib/uucp/uulog -s sky
```

To display the last 40 lines of the file transfer log for host sky, use the -f option and the number option as shown:

```
% /usr/lib/uucp/uulog -f sky -40
```

Table 14-11 summarizes uulog command options and required entries.

# Table 14-11: Options to the uulog Command

| Option | Description |
|---|---|
| -f host | Performs a tail -f on the file transfer log for the specified host, displaying the end of the log file. Use the Interrupt key sequence to leave the file and return to the prompt. |
| -s[host] | Prints information about copy requests involving the specified host. If no host is specified, information is displayed for all hosts. |
| -x[host] | Displays the uuxqt log file for the the specified host. If no host is specified, information is displayed for all hosts. |
| -number | Displays the last number lines of the log file. See the tail(1) reference page for the application of this parameter. |

# 14.8.3 Monitoring UUCP Status

The uumonitor command is helpful for detecting a host whose status has changed due to a backlog of jobs, a temporary shutdown, or a change of either the phone number or login password.

The uumonitor output consists of the following six fields:

+   - Field 1 – host name
+   - Field 2 – number of command files queued for the remote host; if too large (for example, 100-1000, depending on the host), then the cause of the backlog should be determined
+   - Field 3 – number of requests for remote execution from the remote host
+   - Field 4 – result of the most recent attempt to connect to the remote host
+   - Field 5 – number of remote host login failures, not including failed dial attempts; if greater than 20, no further attempts are made
+   - Field 6 – time of last status entry

For more information, see the uumonitor(8) reference page.