+   Time elapsed since the server was up and running

+   The total number of accesses served so far

+   The total bytes transferred so far

+   The number of children serving requests

+   The number of idle children

+   The status of each child, the number of requests that child has performed, and the total number of bytes served by the child

+   Averages giving the number of requests per second, the number of bytes served per second, and the average number of bytes per request

+   The current percentage CPU used by each child and used in total by Apache

+   The current hosts and requests being processed

![](bbox=[0.12, 0.38, 0.17, 0.42])

Some of the above information is only available when you enable displaying of such information using the ExtendedStatus directive, which is discussed later in this section.

Like the `mod_info` module, this module is also not compiled by default in the standard Apache distribution, so you need use the `--enable-status` option with the `configure` script and compile and install Apache.

# Viewing status pages

After you have the `mod_status` module compiled and built into your Apache server, you need to define the URL location that Apache should use to display the information. In other words, you need to tell Apache which URL will bring up the server statistics on your Web browser.

Let’s say that your domain name is `domain.com`, and you want to use the following URL:

```
http://www.domain.com/server-status
```

Using the `<Location ...>` container, you can tell the server that you want it to handle this URL using the server-status handler found in the `mod_status` module. The following will do the job:

```
<Location /server-status>
  SetHandler server-status
  Order deny,allow
  Deny from all
  Allow from 127.0.0.1 .domain.com
  </Location>
```