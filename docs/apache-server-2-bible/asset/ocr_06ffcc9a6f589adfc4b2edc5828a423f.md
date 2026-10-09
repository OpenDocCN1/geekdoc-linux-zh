Here, the *SetHandler* directive sets the handler (*server-status*) for the previously mentioned URL. After you have added the configuration in *httpd.conf*, restart the server and access the URL from a browser. The `<Location...>` container enables you to access the status information from any host in your domain, or from the server itself. Don't forget to change *domain.com* to your real domain name, and also don't forget to include the leading dot.

You can also have the status page update itself automatically using the *http://server/server-status?refresh=N* URL to refresh the page every *N* seconds.

To view extended status information, add the *ExtendedStatus* On directive in the server configuration context. For example, your entire server status-related configuration in *httpd.conf* could look as follows:

```
ExtendedStatus On
<Location /server-status>
SetHandler server-status
Order deny,allow
Deny from all
Allow from 127.0.0.1 .domain.com
</Location>
```

An example of the extended status information is shown here:

```
Apache Server Status for rhcat.netfix.com
Server Version: Apache/2.0.14 (Unix)
Server Built: Mar 14 2001 12:12:28
────────────────────────────────────────────────────────────────────

Current Time: Thursday, 15-Mar-2001 11:05:08 PST
Restart Time: Thursday, 15-Mar-2001 11:02:40 PST
Parent Server Generation: 0
Server uptime: 2 minutes 28 seconds
Total accesses: 17807 – Total Traffic: 529 kB
CPU Usage: ul/3.4 s. 0.3 cu0 cs0 – 117% CPU load
120 requests/sec – 3660 B/second – 30 B/request
4 requests currently being processed, 8 idle servers
\_WKKK\_………
……

Scoreboard Key:
"" Waiting for Connection, "S" Starting up, "R" Reading Request,
"W" Sending Reply, "K" Keepalive (read), "D" DNS Lookup,
"L" Logging, "G" Gracefully finishing, "." Open slot with no current process
```