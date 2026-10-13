
**TABLE 33.6 CONTINUED**

| Specifier | Translates To... |
|---|---|
| `%p` | Server port. |
| `%P` | Process ID of the child that handled the request. |
| `%T` | Number of seconds it took to handle the request. |
| `%U` | The URL path requested. |
| `%v` | Server name. |

The Common Log Format uses the following format string:

```text
"%h %l %u %t \"%r\" %s %b"
```

Listing 33.2 shows sample entries from an access log using the Common Log format.

**LISTING 33.2  SAMPLE ACCESS LOG USING COMMON LOG FORMAT**

```text
200.251.107.134 - - [24/Oct/2000:17:06:38 -0700] "GET / HTTP/1.1" 200 3304
200.251.107.134 - - [24/Oct/2000:17:06:40 -0700] "GET /mor...jpg HTTP/1.1" 200 26625
192.168.1.3 - - [24/Oct/2000:17:23:31 -0700] "GET /robots.txt HTTP/1.0" 404 163
203.93.18.173 - - [24/Oct/2000:17:37:29 -0700] "GET / HTTP/1.1" 200 3304
203.93.18.173 - - [24/Oct/2000:17:37:33 -0700] "GET /mor...jpg HTTP/1.0" 200 26625
203.93.18.173 - - [24/Oct/2000:17:37:33 -0700] "GET /blueball.gif HTTP/1.0" 200 326
203.93.18.173 - - [24/Oct/2000:17:37:45 -0700] "GET /redball.gif HTTP/1.0" 200 326
192.168.1.2 - - [24/Oct/2000:22:17:57 -0700] "GET /starcraft/ HTTP/1.1" 200 3003
192.168.1.2 - - [24/Oct/2000:22:17:59 -0700] "GET /starcraft/starcraft.jpg HTTP/1.1" 200 6780
192.168.1.3 - - [25/Oct/2000:06:56:37 -0700] "GET /david/ball.gif HTTP/1.0" 200 1135
203.93.18.173 - - [25/Oct/2000:14:05:01 -0700] "GET /tim HTTP/1.0" 301 173
```

Many conversion specifiers can include a status indicator to conditionally show the value for that specifier. The status indicator follows the % and consists of a comma-separated list of status codes (optionally preceded by ! for negation). If the request results in the indicated status codes, the value for the specifier is included in the log entry. Otherwise, the specifier is replaced with a dash in the log entry.

Following are some example conversion specifiers with status indicators:

- `%404f` — Logs the filename that the server tried to open when it encountered error 404, Not Found.
- `%!200,304,302r` — Logs the request for anything not returning a valid status.
- `%302{UserAgent}i` — Logs the value of the UserAgent header in the request when the URL is redirected.

To specify a log format, use the directive LogFormat followed by the format string in quotes and a name for that format. If no name is provided, the format string is used as the default format for subsequent logs defined in the configuration file. The following log formats are defined in the default Web server configuration files:

```text
LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\" combined
LogFormat "%h %l %u %t \"%r\" %>s %b" common
LogFormat "%{Referer}i" referrer
LogFormat "%{User-agent}i" agent
```

## USING CLIENT HOSTNAME LOOKUPS

By default, the server logs the address, but not the hostname, of requesting clients when the %h conversion specifier is used in a log format string. Use the HostNameLookups directive to make the server log the hostname instead of the address.

When HostNameLookups is configured to On, the logging software in the server tries to determine the hostname of the requesting client by doing a DNS lookup using the client’s IP address at the time of the request. This adds a considerable amount of overhead for each request that the server processes, so the feature is defaulted to Off. For low traffic sites, it is usually all right to turn this on.

> **Tip**
>
> If you have HostNameLookups turned off, you can use the program logresolve, which comes with Apache to process logs and convert IP addresses to hostnames after the fact. This is usually much more efficient than adding the hostname at the time of each request because logresolve does not have to look up the same IP address over and over again. However, logresolve might not be able to determine some hostnames accurately because some clients might change their name or address between the time of their request and the time that logresolve is run.
>
> To resolve the IP addresses in a log file, use logresolve with the target log file as standard input and the processed log file as standard output. For example, log in as root, switch to the directory `/usr/local/apache/bin`, and type the following:
>
> ```shell
> ./logresolve /usr/local/apache/logs/access_log > /tmp/log_with_names
> ```

## DEFINING ADDITIONAL LOGS

You can define as many transfer logs as you want. When combined with custom log formats, this enables you to divide your log information among different files, which might make it easier to process with log analysis tools.

To define additional logs, use the CustomLog directive. Each CustomLog directive needs to be followed by the name of the log file and a log format string or name (as defined by a LogFormat directive). For example, an agent log (described next) can be defined with the following directives:

```text
LogFormat "%{User-agent}i" agent
CustomLog /usr/local/apache/logs/agent_log agent
```

## AGENT AND REFERRER LOGS

In addition to the transfer log, you can define additional log files to record information about the requests that your server handles. Two other commonly used logs are called the agent log and the referrer log. An agent log is used to record information about the client browser (user agent) that is used to make requests of your system. This information is useful because it enables you to develop a profile of the types of users who are visiting your site. The referrer log is used to record information about what page referred the client to your site (that is, what page held the link that the client followed to get to one of your pages). This is useful for determining how users are getting to your site, which might help you advertise or promote your Web site more effectively.

These logs are defined using the AgentLog and ReferrerLog directives, respectively.

> **Caution**
>
> Note that “Referer” is a misspelling of “referrer,” but because it is now part of the HTML standard, this is the correct spelling for the directive. Occasionally this can cause a lot of confusion. For instance, the default referrer log format in Apache is called “referer,” even though the directive is ReferrerLog.

You can define a log, using LogFormat and CustomLog, to record the same information that goes into either the agent log or the referrer log. In fact, use of the AgentLog directive is now deprecated. However, when you use the ReferrerLog directive to create a referrer log, it allows you one additional capability that the CustomLog method does not—you can use the ReferrerIgnore directive to eliminate a specific set of referrers from the log.

For example, if you use the following line, no record of references from example’s Web site will be included in your log:

```text
ReferrerIgnore www.example.com
```

This can help reduce the size of your log and help you pinpoint new entries in the referrer log.

## ERROR LOG

The error log is a special log that records server status—usually error—events. Use the ErrorLog directive to set the output location for the log. This can include a filename, a pipe to another program, or the syslog daemon. The default definition of the error log is as follows:

```text
ErrorLog /usr/local/apache/logs/error_log
```

To specify a pipe to another program, use a vertical bar in front of the program specification, as follows:

```text
ErrorLog | /usr/local/bin/page_me_at_home.pl
```

To output the error log records to the syslog daemon, use an argument of syslog, as in the following:

```text
ErrorLog syslog
```

You can use the LogLevel directive to control the verbosity of the error log. Table 33.7 shows the list of available log levels and their descriptions.

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

## SCRIPT LOG

The server supports another special log specifically to aid in debugging CGI scripts. This is the script log. A script log holds information about the parameters, input, and output to a CGI script when the script fails. Debugging CGI scripts has historically been difficult because the server silently discards the context of the request and output of the script. The script log is a fairly recent addition to the Web server, which makes debugging scripts much easier.

To define a script log, specify the log name with the ScriptLog directive. When a CGI script runs on your system and fails, the following information is logged:

- Time of the failure
- Request line from the client
- HTTP status code
- CGI script filename
- An error message, if the script failed to run
- HTTP headers received in the request
- HTTP headers produced by the CGI script
- CGI script standard output
- CGI script standard input

Using this information, you can probably track down problems with the CGI script in question. Many problems with CGI scripts come from improperly formatted response headers.

Note that a script log is intended for debugging use only. It creates overhead that is not appropriate for a Web server in production use. Also, because of the amount of information logged on
