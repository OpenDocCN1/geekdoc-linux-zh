# Support Programs

Apache includes a number of additional programs to support the Web administrator. These binaries are installed in the \textbf{bin}/ subdirectory of the server root directory. The most important of these is \textbf{apachectl}, which controls the manual stopping and starting of the \textbf{httpd} daemon, as well as validation of the \textbf{httpd.conf} configuration file. Apache may be stopped and started with

```
# /usr/HTTPServer/bin/apachectl stop
# /usr/HTTPServer/bin/apachectl start
```

Additionally, after making modifications to the configuration file, it is a good idea to validate the changes:

```
# /usr/HTTPServer/bin/apachectl configtest
```

A bad configuration file will prevent a running server from restarting, causing unwanted downtime while the error is researched and corrected. After a successful validation, it is safe to restart a running server:

```
# /usr/HTTPServer/bin/apachectl restart
```

The \textbf{rotatelogs} program is another helpful tool. As the name suggests, it helps to manage what can be voluminous Web logs. The most common way to use this program is by calling it from within the \textbf{httpd.conf} file itself. The details of how to do this are discussed in the section “Managing Logs” later in this chapter.

# Virtual Server Configuration

\textit{Virtual hosts} are a popular feature of Apache that allows the administrator to run multiple Web sites from one server. Virtual hosts come in two types: name-based and IP address based. IP-based virtual hosts require a separate IP address for each host. This can usually be achieved with IP aliases on one physical network interface. In contrast, name-based virtual hosts may share one IP address; all DNS records for these hosts refer to the same IP address. The name-based virtual host relies on the client to send an HTTP/1.1 header identifying the name of the host it is trying to contact. Most browsers now support HTTP/1.1, making name-based virtual hosts a viable and practical option. The exception to this is secure servers; secure servers require matching reverse DNS lookups. Example 18-6 shows a name-based virtual host configuration. An example of an IP-based virtual host appears in the next section.

# Example 18-6

```
NameVirtualHost *
<VirtualHost **>
ServerName accounting.wine.edu
DocumentRoot /var/data/accounting.wine.edu
```