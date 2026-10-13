cerned. To make sure that only machines on your domain can access the status page, replace the preceding configuration with the following:

```
<Location /apache-status>
SetHandler server-status
order deny, allow
deny from all
allow from .yourdomain.com
</Location>
```

where yourdomain.com should be replaced with your own domain name. If you want only one or more selected hosts to have access to this page, simply list the host names in the allow directive line.

Tip
You can have the status page update itself automatically if you have a browser that supports the refresh command. Access the page http://www.yourdomain.com/server-status?refresh=N to refresh the page every N seconds.

To simplify the status display, add ?auto at the end of the URL. This query string tells Apache to display simplified output.

# Logging hits and errors

By default, the standard Apache distribution includes a module called mod_log_config, which is responsible for the basic logging, and writes Common Log Format (CLF) log files by default. You can alter this behavior by using the LogFormat directive. However, CLF covers logging requirements in most environments.

The CLF file contains a separate line for each request. A line is composed of several tokens separated by spaces:

host ident authuser date request status bytes

If a token does not have a value, then it is represented by a hyphen (-). Tokens have the following meanings:

+   - **Host.** The fully qualified domain name of the client, or its IP address.