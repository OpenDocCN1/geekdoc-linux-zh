| Level | Description |
|---|---|
| emerg | Emergency—system is unusable |
| alert | Action needs to be taken immediately |
| crit | Critical condition |
| error | Error |
| warn | Warning conditions |
| notice | Normal, but important, event |
| info | Information message |
| debug | Debugging messages |

The levels in the table are shown in order of decreasing event importance. If LogLevel is not defined, the level error is used. The default value of LogLevel is warn.

# SCRIPT LOG

The server supports another special log specifically to aid in debugging CGI scripts. This is the script log. A script log holds information about the parameters, input, and output to a CGI script when the script fails. Debugging CGI scripts has historically been difficult because the server silently discards the context of the request and output of the script. The script log is a fairly recent addition to the Web server, which makes debugging scripts much easier.

To define a script log, specify the log name with the ScriptLog directive. When a CGI script runs on your system and fails, the following information is logged:

+   - Time of the failure
+   - Request line from the client
+   - HTTP status code
+   - CGI script filename
+   - An error message, if the script failed to run
+   - HTTP headers received in the request
+   - HTTP headers produced by the CGI script
+   - CGI script standard output
+   - CGI script standard input

Using this information, you can probably track down problems with the CGI script in question. Many problems with CGI scripts come from improperly formatted response headers.

Note that a script log is intended for debugging use only. It creates overhead that is not appropriate for a Web server in production use. Also, because of the amount of information logged on