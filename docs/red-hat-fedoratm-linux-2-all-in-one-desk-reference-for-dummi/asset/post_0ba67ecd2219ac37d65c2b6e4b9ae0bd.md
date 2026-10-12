
## Performance Tuning

On this tab, you can set some parameters that control overall performance. You can set the maximum number of connections allowed, the timeout period for connections, and the maximum number of requests per connection.

![](img/9f89727199836b0f871f1745838aa8b2_649_0.png)

Initially the configuration window displays the default values from the configuration file /etc/httpd/conf/httpd.conf. After you make any changes, click the Ok button. The configuration tool prompts you to ask whether you really want to save the changes and exit. If you do, click Yes and you are done.

**REMEMBER**

When you configure the Apache HTTP server from this configuration tool, all you’re doing is changing options and attributes stored in the /etc/httpd/conf/httpd.conf file. You can just as easily make the changes by editing the configuration file, which is a plain text file. In the next section, I introduce you to some common configuration directives in the Apache configuration file.

### Apache configuration files

The Apache server’s operation is controlled by the httpd.conf configuration file located in the /etc/httpd/conf/ directory. This file controls how the server runs, what documents it serves, and who can access these documents.

In the next few sections, I summarize key information about the httpd.conf configuration file. Typically, you don’t have to change anything in the configuration files to run the Apache Web server. However, knowing the format of the configuration files and the meaning of the various keywords used in them is useful.

As you study the configuration files in the `/etc/httpd/conf` directory, keep these syntax rules in mind:

- Each configuration file is a text file that you can edit with your favorite text editor and view with the `more` command.
- All comment lines begin with a `#`.
- Each line can have only one directive.
- Extra spaces and blank lines are ignored.
- All entries, except pathnames and URLs, are case insensitive.

### The `httpd.conf` configuration file

The `/etc/httpd/conf/httpd.conf` file is the main HTTP-daemon configuration file — it includes directives that control how the Apache Web server runs. For example, the `httpd.conf` file specifies the port number the server uses, the name of the Web site, and the e-mail address to which mail is sent in case of any problems with the server. In addition, `httpd.conf` also includes information on where the Web pages are located and who can access what directories.

In the following sections, I present the Apache directives grouped in three separate categories: general HTTPD directives, resource-configuration directives, and access-control directives. Finally, I explain how virtual hosts can be set up in Apache Web server so a single Web server can handle Web requests sent to several IP addresses or host names.

To browse the Apache HTTPD documentation online, visit [httpd.apache.org/docs-2.0/](http://httpd.apache.org/docs-2.0/). Specifically, you can look up information on configuration directives at [httpd.apache.org/docs-2.0/mod/directives.html](http://httpd.apache.org/docs-2.0/mod/directives.html).

### General HTTPD directives

Some interesting items from the `httpd.conf` file are:

- `ServerName` specifies the host name of your Web site (of the form `www.your.domain`) and the port number where the Web server accepts connections. `ServerName` is used only when redirecting a Web page to another Web page. The name is a registered domain name other users can locate through their name servers. Here is an example:
  ```
  ServerName www.myhost.com:80
  ```
  If you don't have a registered domain name, use the IP address of your Fedora Core system.

- `ServerAdmin` is the e-mail address that the Web server provides to clients in case any errors occur. The default value for `ServerAdmin` is `root@localhost`. Set this address to a valid e-mail address that anyone on the Internet can use to report errors to Web site contains.

- `Include` loads more configuration directives from a specified file. For example, the default `/etc/httpd/conf/httpd.conf` file loads all the configuration files from the `/etc/httpd/conf.d` directory by using the following `Include` directive:
  `Include conf.d/*.conf`
  This command means that you can load another set of configurations by simply adding a file to the `/etc/httpd/conf.d` directory. In fact, that's the directory where you find the configuration files for various Apache HTTPD modules, such as Perl, PHP, and SSL. Study the configuration file in the `/etc/httpd/conf.d` directory to find out more about the total set of directives that affect the Apache Web server's behavior.

Many more directives control the way that the Apache Web server works. The following list summarizes some of the directives you can use in the `httpd.conf` file. You can leave most of these directives in their default settings, but know about them if you're maintaining a Web server is important.

- `Listen IP-Address:Port`: Forces the Web server to listen to a specific IP address and port number. By default, the Web server responds to all IP addresses associated with the host.

- `User name [#id]`: Specifies the username (or ID) the HTTP daemon uses. You can leave this directive at the default setting (`apache`). If you specify a user ID, use a hash (#) prefix for the numeric ID.

- `Group name [#id]`: Specifies the group name (or ID) of the HTTP daemon when running in stand-alone mode. The default group name is `apache`.

- `ServerRoot pathname`: Specifies the directory where the Web server is located. By default, the configuration and log files are expected to reside in subdirectories of this directory. In Fedora Core, `ServerRoot` is set to `/etc/httpd`.

- `ServerName www.company.com:80`: Sets the server's host name to `www.company.com` and the port number to 80. `ServerName` is used only when redirecting a Web page to another.

- `ServerTokens Major|Minor|Min|Prod|OS|Full`: Controls how much information is sent back to the client in the `Server` field of the header. Set the directive to `Prod` for a `Server` response that simply identifies the product name (in this case, `Apache`).

![](img/9f89727199836b0f871f1745838aa8b2_651_0.png)

- `StartServers num`: Sets the number of child processes that start as soon as the Apache Web server runs. The default value is 8.

- `MaxSpareServers num`: Sets the desired maximum number of idle child-server processes (a child process is considered idle if it's not handling an HTTP request). The default value is 20.

- `MinSpareServers num`: Sets the desired minimum number of idle child server processes (a child process is considered idle if it's not handling an HTTP request). A new spare process is created every second if the number falls below this threshold. The default value is 5.

- `Timeout numsec`: Sets the number of seconds that the server waits for a client to send a query after the client establishes connection. The default Timeout is 300 seconds (five minutes).

- `ErrorLog filename`: Sets the file where `httpd` logs the errors it encounters. If the filename does not begin with a slash (/), the name is taken to be relative to `ServerRoot`. The default `ErrorLog` is `/etc/httpd/logs/error_log`, but `/etc/httpd/logs` is a symbolic link to the `/var/log/httpd` directory. Therefore the log files are in `/var/log/httpd` directory. Typical error-log entries include events, such as server restarts, and any warning messages, such as the following:
  ```
  [Sat Mar 13 18:10:01 2004] [notice] Apache/2.0.48 (Fedora) configured --
  resuming normal operations
  [Sat Mar 13 18:10:37 2004] [error] [client 192.168.0.3] File does not exist: /var/www/html/book
  ```

- `TransferLog filename`: Sets the file where `httpd` records all client accesses (including failed accesses). The default `TransferLog` is `/var/log/httpd/access_log`. The following example shows how a typical access is recorded in this log file:
  ```
  192.168.0.3 - - [13/Mar/2004:18:10:23 -0500] "GET / HTTP/1.1" 200 3888 "-" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; .NET CLR 1.1.4322)"
  192.168.0.3 - - [13/Mar/2004:18:10:23 -0500] "GET /icons/apache_pb2.gif HTTP/1.1" 200 244 "/192.168.0.6" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT5.1; (R1 1.3); .NET CLR 1.1.4322)"
  192.168.0.3 - - [13/Mar/2004:18:10:23 -0500] "GET /icons/powered_by_fedora.png HTTP/1.1" 200 2243 "http://192.168.0.6/" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; (R1 1.3); .NET CLR 1.1.4322)"
  ```

- `LogFormat formatstring formatname`: Specifies the format of log-file entries for the `TransferLog`. The `CustomLog` directive also uses this format to produce logs in a specific format.

- `CustomLog filename formatname`: Sets the name of the custom log file where `httpd` records all client accesses (including failed accesses) in a format specified by `formatname` (which you define using a `LogFormat` directive).
