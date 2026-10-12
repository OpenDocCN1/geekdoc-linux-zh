
His complete e-mail address is jdoe@someplace.net. Given that address, anyone on the Internet can send e-mail to John Doe.

他的完整电子邮件地址是 jdoe@someplace.net。凭借该地址，互联网上的任何人都可以向 John Doe 发送电子邮件。

To set up and use e-mail on your Red Hat Linux PC, you need two types of mail software:

设置和使用 Red Hat Linux PC 上的电子邮件，您需要两种类型的邮件软件：

- *Mail-user agent* software enables you to read your mail messages, write replies, and compose new messages. Typically, the mail-user agent retrieves messages from the mail server using POP3 or IMAP4 protocol. POP3 is the Post Office Protocol version 3 and IMAP4 is the Internet Message Access Protocol version 4. The Red Hat Linux CD-ROMs include several popular mail user agents such as `pine` and `elm`.
- *邮件用户代理* 软件使您能够阅读邮件消息、撰写回复并编写新消息。通常，邮件用户代理使用 POP3 或 IMAP4 协议从邮件服务器检索消息。POP3 是邮局协议版本 3，IMAP4 是 Internet 消息访问协议版本 4。Red Hat Linux CD-ROM 包含多个流行的邮件用户代理，例如 `pine` 和 `elm`。
- *Mail-transport agent* software actually sends and receives mail-message text. The exact method used for mail transport depends on the underlying network. In TCP/IP networks, the mail-transport agent delivers mail using the Simple Mail Transfer Protocol (SMTP). This book’s Red Hat Linux CD-ROMs include `sendmail`, a powerful and popular mail-transport agent for TCP/IP networks.
- *邮件传输代理* 软件实际发送和接收邮件消息文本。邮件传输所使用的方法取决于底层网络。在 TCP/IP 网络中，邮件传输代理使用简单邮件传输协议（SMTP）投递邮件。本书的 Red Hat Linux CD-ROM 包含 `sendmail`，这是一款功能强大且流行的 TCP/IP 网络邮件传输代理。

Most mail-transport agents run as *daemons* — background processes that run as long as your system is up. Because you or another user on the system can send mail at any time, the transport agent has to be there to deliver the mail to its destination. The mail-user agent runs only when the user wants to check mail.

大多数邮件传输代理作为 *守护进程* 运行——只要系统处于运行状态就会持续运行的后台进程。因为您或系统上的其他用户可以在任何时候发送邮件，所以传输代理必须存在以将邮件投递到目的地。邮件用户代理仅在用户想要检查邮件时运行。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_190_0.png)

Typically, a mail-transport agent starts after the system boots. The system startup files for Red Hat Linux are set up so that the sendmail mail-transport agent starts when the Linux system is in multiuser mode. The shell script file `/etc/rc.d/init.d/sendmail` starts sendmail.

通常，邮件传输代理在系统启动后启动。Red Hat Linux 的系统启动文件设置成在 Linux 系统处于多用户模式时启动 sendmail 邮件传输代理。shell 脚本文件 `/etc/rc.d/init.d/sendmail` 启动 sendmail。

Because the system is already set up to start sendmail at boot time, all you have to do is use an appropriate sendmail configuration file to get e-mail going on your Linux system.

由于系统已设置在启动时启动 sendmail，您所需要做的就是使用合适的 sendmail 配置文件来在 Linux 系统上启用电子邮件。

You cannot send or receive e-mail until the sendmail mail-transport agent is configured properly. The sendmail transport agent has the reputation of being a complex, but complete, mail-delivery system. If you take a quick look at sendmail’s configuration file, `/etc/sendmail.cf`, you can see that sendmail is indeed complex. Luckily, you do not have to be an expert on the sendmail configuration file. All you need is the predefined configuration files from this book’s companion CD-ROMs.

在 sendmail 邮件传输代理正确配置之前，您无法发送或接收电子邮件。sendmail 传输代理以复杂但完整的邮件投递系统而闻名。如果您快速查看 sendmail 的配置文件 `/etc/sendmail.cf`，您会发现 sendmail 确实很复杂。幸运的是，您不必是 sendmail 配置文件的专家。您只需要本书附带 CD-ROM 上的预定义配置文件即可。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_191_0.png)

If you install the Mail/WWW/News Tools component during Red Hat Linux installation (see Session 3), your system should have a working sendmail configuration file — /etc/sendmail.cf. The default file assumes an Internet connection and a name server. Provided you have an Internet connection, you should be able to send and receive e-mail from your Linux PC once you connect it to the Internet. Then you can use a mail-user agent such as elm to compose and send mail messages.

如果您在 Red Hat Linux 安装期间安装 Mail/WWW/News Tools 组件（参见第 3 节），您的系统应该具有可用的 sendmail 配置文件 — /etc/sendmail.cf。默认文件假定存在 Internet 连接和名称服务器。只要您拥有 Internet 连接，在将 Linux PC 连接到 Internet 后，您应该能够发送和接收电子邮件。然后您可以使用诸如 elm 之类的邮件用户代理来撰写和发送邮件消息。

## Setting Up the Apache Web Server

## 设置 Apache Web 服务器

You probably already know how it feels to use the Web, but you may not know how to set up a Web server so that you, too, can provide information to the world through Web pages. To become an information provider on the Web, you have to run a Web server on your Red Hat Linux PC on the Internet.

您可能已经知道使用 Web 的感觉，但您可能不知道如何设置 Web 服务器，以便您也可以通过网页向世界提供信息。要成为 Web 上的信息提供者，您必须在 Internet 上的 Red Hat Linux PC 上运行 Web 服务器。

Web servers provide information by using HTTP. Web servers are also known as HTTP daemons (because continuously running server processes are called daemons in UNIX), or HTTPD for short. The Web server program usually is named httpd.

Web 服务器通过使用 HTTP 提供信息。Web 服务器也被称为 HTTP 守护进程（因为在 UNIX 中持续运行的服务器进程称为守护进程），简称为 HTTPD。Web 服务器程序通常命名为 httpd。

Among the freely available Web servers, Apache Web server is the most popular. Apache is freely available over the Internet and it accompanies Red Hat Linux on this book’s companion CD-ROMs.

在可自由获得的 Web 服务器中，Apache Web 服务器是最受欢迎的。Apache 可通过 Internet 免费获得，并随本书附带的 CD-ROM 上的 Red Hat Linux 一起提供。

When you install Red Hat Linux from this book’s companion CD-ROMs, you also have the option of installing the Apache Web server. If you install the Mail/WWW/News Tools package during Red Hat Linux installation, then Red Hat Linux automatically starts the Apache Web server during system boot.

当您从本书附带的 CD-ROM 安装 Red Hat Linux 时，您也可以选择安装 Apache Web 服务器。如果您在 Red Hat Linux 安装期间安装 Mail/WWW/News Tools 软件包，则 Red Hat Linux 会在系统启动期间自动启动 Apache Web 服务器。

Perform the following steps to verify that the Apache Web server software is installed and running on your system:

执行以下步骤以验证 Apache Web 服务器软件是否已安装并在您的系统上运行：

1. Type the following command to check whether the Apache Web server is installed:
```
rpm -q apache
```
apache-1.3.12-21

If the output shows an apache package name, you have the Apache software installed on your system.
1. 输入以下命令检查 Apache Web 服务器是否已安装：
```
rpm -q apache
```
apache-1.3.12-21

如果输出显示 apache 软件包名称，则表示您的系统已安装 Apache 软件。

2. Type the following command to check whether the httpd process (the name of the Apache Web server program is httpd) is running:
```
ps ax | grep httpd
```

The output should show a number of httpd processes. It is common to run several Web server processes — one parent and several child processes — so that several HTTP requests can be handled efficiently by assigning each request to an httpd process.
2. 输入以下命令检查 httpd 进程（Apache Web 服务器程序的名称为 httpd）是否正在运行：
```
ps ax | grep httpd
```

输出应显示多个 httpd 进程。通常运行多个 Web 服务器进程——一个父进程和多个子进程——以便通过将每个请求分配给一个 httpd 进程来高效处理多个 HTTP 请求。

3. Use the telnet program on your Linux system and employ the HTTP HEAD command to query the Web server as follows:
```
telnet localhost 80
Trying 128.0.0.1...
Connected to localhost.
Escape character is '^]'.
HEAD / HTTP/1.0
... Press Enter once more to type a blank line
HTTP/1.1 200 OK
Date: Sat, 19 Aug 2000 23:57:14 GMT
Server: Apache/1.3.12 (Unix)  (Red Hat/Linux)
Last-Modified: Mon, 07 Aug 2000 10:21:07 GMT
ETag: "328fe-b4a-398e8d93"
Accept-Ranges: bytes
Content-Length: 2890
Connection: close
Content-Type: text/html

Connection closed by foreign host.
```

If you get a response such as the preceding, your system already has the Apache Web server installed and set up correctly. All you have to do is understand the configuration so that you can place the HTML documents in the proper directory.
3. 在 Linux 系统上使用 telnet 程序并按如下方式使用 HTTP HEAD 命令查询 Web 服务器：
```
telnet localhost 80
Trying 128.0.0.1...
Connected to localhost.
Escape character is '^]'.
HEAD / HTTP/1.0
... Press Enter once more to type a blank line
HTTP/1.1 200 OK
Date: Sat, 19 Aug 2000 23:57:14 GMT
Server: Apache/1.3.12 (Unix)  (Red Hat/Linux)
Last-Modified: Mon, 07 Aug 2000 10:21:07 GMT
ETag: "328fe-b4a-398e8d93"
Accept-Ranges: bytes
Content-Length: 2890
Connection: close
Content-Type: text/html

Connection closed by foreign host.
```

如果您得到与上述类似的响应，则表示您的系统已正确安装并设置了 Apache Web 服务器。您所需要做的就是了解配置，以便将 HTML 文档放置在正确的目录中。

4. Use a Web server to load the home page from your system. Start Netscape Navigator by clicking the big “N” icon on the GNOME Panel, use the URL http://localhost/, and then see what happens. You should see a Web page with the title “Test Page for the Apache Web Server on Red Hat Linux.”
4. 使用 Web 服务器从系统加载主页。单击 GNOME 面板上的大“N”图标启动 Netscape Navigator，使用 URL http://localhost/，然后查看会发生什么。您应该会看到标题为“Test Page for the Apache Web Server on Red Hat Linux”的网页。

The Apache Web server is set up to serve the HTML documents from the /var/www/html directory. Therefore, you should place your Web pages in the /var/www/html directory. In particular, edit or replace the /var/www/html/index.html file with your own home page.

Apache Web 服务器设置为从 /var/www/html 目录提供 HTML 文档。因此，您应该将网页放置在 /var/www/html 目录中。特别是，用您自己的主页编辑或替换 /var/www/html/index.html 文件。

In addition to the HTML files, the Apache Web server also supports Common Gateway Interface (CGI) programs — programs that the Web server can invoke to access other files and databases. You should place any CGI programs in the /var/www/cgi-bin directory.

除了 HTML 文件外，Apache Web 服务器还支持通用网关接口（CGI）程序——Web 服务器可以调用的程序来访问其他文件和数据库。您应该将任何 CGI 程序放置在 /var/www/cgi-bin 目录中。

Also note the following useful information about the Apache Web server:

另请注意有关 Apache Web 服务器的以下有用信息：

- The Apache Web server configuration files are located in the /etc/httpd/conf directory. There are three configuration files, access.conf, httpd.conf, and srm.conf. These configuration files control how the server runs, what documents it serves, and who can access these documents.
- Apache Web 服务器配置文件位于 /etc/httpd/conf 目录。有三个配置文件，access.conf、httpd.conf 和 srm.conf。这些配置文件控制服务器如何运行、提供哪些文档以及谁可以访问这些文档。
- The /var/log/httpd directory is where the Apache Web server’s log files (access logs and error logs) are located.
- /var/log/httpd 目录是 Apache Web 服务器日志文件（访问日志和错误日志）所在的位置。
- The /etc/rc.d/init.d/httpd script starts the httpd process as your Red Hat Linux system boots.
- /etc/rc.d/init.d/httpd 脚本在 Red Hat Linux 系统启动时启动 httpd 进程。

## Setting Up the FTP Server

## 设置 FTP 服务器

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_193_0.png)

Besides e-mail and Web, anonymous FTP is a common service on an Internet host. You may be familiar with FTP, which you can use to transfer files from one system to another on the Internet. When you use FTP to transfer files to or from a remote system, you have to log in to the remote system before you can use FTP.

除了电子邮件和 Web 之外，匿名 FTP 是 Internet 主机上的常见服务。您可能熟悉 FTP，您可以使用它在 Internet 上从一个系统向另一个系统传输文件。当您使用 FTP 向远程系统传输文件或从远程系统传输文件时，您必须先登录到远程系统，然后才能使用 FTP。

If you install Red Hat Linux from this book’s companion CD-ROMs, you should have anonymous FTP set up on your system and the FTP server configured to run when needed. The default setup also employs the necessary security precautions.

如果您从本书附带的 CD-ROM 安装 Red Hat Linux，您应该已在系统上设置了匿名 FTP，并且 FTP 服务器配置为在需要时运行。默认设置还采用了必要的[content]
His complete e-mail address is jdoe@someplace.net. Given that address, anyone on the Internet can send e-mail to John Doe.

他的完整电子邮件地址是 jdoe@someplace.net。凭借该地址，互联网上的任何人都可以向 John Doe 发送电子邮件。

To set up and use e-mail on your Red Hat Linux PC, you need two types of mail software:

设置和使用 Red Hat Linux PC 上的电子邮件，您需要两种类型的邮件软件：

- *Mail-user agent* software enables you to read your mail messages, write replies, and compose new messages. Typically, the mail-user agent retrieves messages from the mail server using POP3 or IMAP4 protocol. POP3 is the Post Office Protocol version 3 and IMAP4 is the Internet Message Access Protocol version 4. The Red Hat Linux CD-ROMs include several popular mail user agents such as `pine` and `elm`.
- *邮件用户代理* 软件使您能够阅读邮件消息、撰写回复并编写新消息。通常，邮件用户代理使用 POP3 或 IMAP4 协议从邮件服务器检索消息。POP3 是邮局协议版本 3，IMAP4 是 Internet 消息访问协议版本 4。Red Hat Linux CD-ROM 包含多个流行的邮件用户代理，例如 `pine` 和 `elm`。
- *Mail-transport agent* software actually sends and receives mail-message text. The exact method used for mail transport depends on the underlying network. In TCP/IP networks, the mail-transport agent delivers mail using the Simple Mail Transfer Protocol (SMTP). This book’s Red Hat Linux CD-ROMs include `sendmail`, a powerful and popular mail-transport agent for TCP/IP networks.
- *邮件传输代理* 软件实际发送和接收邮件消息文本。邮件传输所使用的方法取决于底层网络。在 TCP/IP 网络中，邮件传输代理使用简单邮件传输协议（SMTP）投递邮件。本书的 Red Hat Linux CD-ROM 包含 `sendmail`，这是一款功能强大且流行的 TCP/IP 网络邮件传输代理。

Most mail-transport agents run as *daemons* — background processes that run as long as your system is up. Because you or another user on the system can send mail at any time, the transport agent has to be there to deliver the mail to its destination. The mail-user agent runs only when the user wants to check mail.

大多数邮件传输代理作为 *守护进程* 运行——只要系统处于运行状态就会持续运行的后台进程。因为您或系统上的其他用户可以在任何时候发送邮件，所以传输代理必须存在以将邮件投递到目的地。邮件用户代理仅在用户想要检查邮件时运行。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_190_0.png)

Typically, a mail-transport agent starts after the system boots. The system startup files for Red Hat Linux are set up so that the sendmail mail-transport agent starts when the Linux system is in multiuser mode. The shell script file `/etc/rc.d/init.d/sendmail` starts sendmail.

通常，邮件传输代理在系统启动后启动。Red Hat Linux 的系统启动文件设置成在 Linux 系统处于多用户模式时启动 sendmail 邮件传输代理。shell 脚本文件 `/etc/rc.d/init.d/sendmail` 启动 sendmail。

Because the system is already set up to start sendmail at boot time, all you have to do is use an appropriate sendmail configuration file to get e-mail going on your Linux system.

由于系统已设置在启动时启动 sendmail，您所需要做的就是使用合适的 sendmail 配置文件来在 Linux 系统上启用电子邮件。

You cannot send or receive e-mail until the sendmail mail-transport agent is configured properly. The sendmail transport agent has the reputation of being a complex, but complete, mail-delivery system. If you take a quick look at sendmail’s configuration file, `/etc/sendmail.cf`, you can see that sendmail is indeed complex. Luckily, you do not have to be an expert on the sendmail configuration file. All you need is the predefined configuration files from this book’s companion CD-ROMs.

在 sendmail 邮件传输代理正确配置之前，您无法发送或接收电子邮件。sendmail 传输代理以复杂但完整的邮件投递系统而闻名。如果您快速查看 sendmail 的配置文件 `/etc/sendmail.cf`，您会发现 sendmail 确实很复杂。幸运的是，您不必是 sendmail 配置文件的专家。您只需要本书附带 CD-ROM 上的预定义配置文件即可。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_191_0.png)

If you install the Mail/WWW/News Tools component during Red Hat Linux installation (see Session 3), your system should have a working sendmail configuration file — /etc/sendmail.cf. The default file assumes an Internet connection and a name server. Provided you have an Internet connection, you should be able to send and receive e-mail from your Linux PC once you connect it to the Internet. Then you can use a mail-user agent such as elm to compose and send mail messages.

如果您在 Red Hat Linux 安装期间安装 Mail/WWW/News Tools 组件（参见第 3 节），您的系统应该具有可用的 sendmail 配置文件 — /etc/sendmail.cf。默认文件假定存在 Internet 连接和名称服务器。只要您拥有 Internet 连接，在将 Linux PC 连接到 Internet 后，您应该能够发送和接收电子邮件。然后您可以使用诸如 elm 之类的邮件用户代理来撰写和发送邮件消息。

## Setting Up the Apache Web Server

## 设置 Apache Web 服务器

You probably already know how it feels to use the Web, but you may not know how to set up a Web server so that you, too, can provide information to the world through Web pages. To become an information provider on the Web, you have to run a Web server on your Red Hat Linux PC on the Internet.

您可能已经知道使用 Web 的感觉，但您可能不知道如何设置 Web 服务器，以便您也可以通过网页向世界提供信息。要成为 Web 上的信息提供者，您必须在 Internet 上的 Red Hat Linux PC 上运行 Web 服务器。

Web servers provide information by using HTTP. Web servers are also known as HTTP daemons (because continuously running server processes are called daemons in UNIX), or HTTPD for short. The Web server program usually is named httpd.

Web 服务器通过使用 HTTP 提供信息。Web 服务器也被称为 HTTP 守护进程（因为在 UNIX 中持续运行的服务器进程称为守护进程），简称为 HTTPD。Web 服务器程序通常命名为 httpd。

Among the freely available Web servers, Apache Web server is the most popular. Apache is freely available over the Internet and it accompanies Red Hat Linux on this book’s companion CD-ROMs.

在可自由获得的 Web 服务器中，Apache Web 服务器是最受欢迎的。Apache 可通过 Internet 免费获得，并随本书附带的 CD-ROM 上的 Red Hat Linux 一起提供。

When you install Red Hat Linux from this book’s companion CD-ROMs, you also have the option of installing the Apache Web server. If you install the Mail/WWW/News Tools package during Red Hat Linux installation, then Red Hat Linux automatically starts the Apache Web server during system boot.

当您从本书附带的 CD-ROM 安装 Red Hat Linux 时，您也可以选择安装 Apache Web 服务器。如果您在 Red Hat Linux 安装期间安装 Mail/WWW/News Tools 软件包，则 Red Hat Linux 会在系统启动期间自动启动 Apache Web 服务器。

Perform the following steps to verify that the Apache Web server software is installed and running on your system:

执行以下步骤以验证 Apache Web 服务器软件是否已安装并在您的系统上运行：

1. Type the following command to check whether the Apache Web server is installed:
```
rpm -q apache
```
apache-1.3.12-21

If the output shows an apache package name, you have the Apache software installed on your system.
1. 输入以下命令检查 Apache Web 服务器是否已安装：
```
rpm -q apache
```
apache-1.3.12-21

如果输出显示 apache 软件包名称，则表示您的系统已安装 Apache 软件。

2. Type the following command to check whether the httpd process (the name of the Apache Web server program is httpd) is running:
```
ps ax | grep httpd
```

The output should show a number of httpd processes. It is common to run several Web server processes — one parent and several child processes — so that several HTTP requests can be handled efficiently by assigning each request to an httpd process.
2. 输入以下命令检查 httpd 进程（Apache Web 服务器程序的名称为 httpd）是否正在运行：
```
ps ax | grep httpd
```

输出应显示多个 httpd 进程。通常运行多个 Web 服务器进程——一个父进程和多个子进程——以便通过将每个请求分配给一个 httpd 进程来高效处理多个 HTTP 请求。

3. Use the telnet program on your Linux system and employ the HTTP HEAD command to query the Web server as follows:
```
telnet localhost 80
Trying 128.0.0.1...
Connected to localhost.
Escape character is '^]'.
HEAD / HTTP/1.0
... Press Enter once more to type a blank line
HTTP/1.1 200 OK
Date: Sat, 19 Aug 2000 23:57:14 GMT
Server: Apache/1.3.12 (Unix)  (Red Hat/Linux)
Last-Modified: Mon, 07 Aug 2000 10:21:07 GMT
ETag: "328fe-b4a-398e8d93"
Accept-Ranges: bytes
Content-Length: 2890
Connection: close
Content-Type: text/html

Connection closed by foreign host.
```

If you get a response such as the preceding, your system already has the Apache Web server installed and set up correctly. All you have to do is understand the configuration so that you can place the HTML documents in the proper directory.
3. 在 Linux 系统上使用 telnet 程序并按如下方式使用 HTTP HEAD 命令查询 Web 服务器：
```
telnet localhost 80
Trying 128.0.0.1...
Connected to localhost.
Escape character is '^]'.
HEAD / HTTP/1.0
... Press Enter once more to type a blank line
HTTP/1.1 200 OK
Date: Sat, 19 Aug 2000 23:57:14 GMT
Server: Apache/1.3.12 (Unix)  (Red Hat/Linux)
Last-Modified: Mon, 07 Aug 2000 10:21:07 GMT
ETag: "328fe-b4a-398e8d93"
Accept-Ranges: bytes
Content-Length: 2890
Connection: close
Content-Type: text/html

Connection closed by foreign host.
```

如果您得到与上述类似的响应，则表示您的系统已正确安装并设置了 Apache Web 服务器。您所需要做的就是了解配置，以便将 HTML 文档放置在正确的目录中。

4. Use a Web server to load the home page from your system. Start Netscape Navigator by clicking the big “N” icon on the GNOME Panel, use the URL http://localhost/, and then see what happens. You should see a Web page with the title “Test Page for the Apache Web Server on Red Hat Linux.”
4. 使用 Web 服务器从系统加载主页。单击 GNOME 面板上的大“N”图标启动 Netscape Navigator，使用 URL http://localhost/，然后查看会发生什么。您应该会看到标题为“Test Page for the Apache Web Server on Red Hat Linux”的网页。

The Apache Web server is set up to serve the HTML documents from the /var/www/html directory. Therefore, you should place your Web pages in the /var/www/html directory. In particular, edit or replace the /var/www/html/index.html file with your own home page.

Apache Web 服务器设置为从 /var/www/html 目录提供 HTML 文档。因此，您应该将网页放置在 /var/www/html 目录中。特别是，用您自己的主页编辑或替换 /var/www/html/index.html 文件。

In addition to the HTML files, the Apache Web server also supports Common Gateway Interface (CGI) programs — programs that the Web server can invoke to access other files and databases. You should place any CGI programs in the /var/www/cgi-bin directory.

除了 HTML 文件外，Apache Web 服务器还支持通用网关接口（CGI）程序——Web 服务器可以调用的程序来访问其他文件和数据库。您应该将任何 CGI 程序放置在 /var/www/cgi-bin 目录中。

Also note the following useful information about the Apache Web server:

另请注意有关 Apache Web 服务器的以下有用信息：

- The Apache Web server configuration files are located in the /etc/httpd/conf directory. There are three configuration files, access.conf, httpd.conf, and srm.conf. These configuration files control how the server runs, what documents it serves, and who can access these documents.
- Apache Web 服务器配置文件位于 /etc/httpd/conf 目录。有三个配置文件，access.conf、httpd.conf 和 srm.conf。这些配置文件控制服务器如何运行、提供哪些文档以及谁可以访问这些文档。
- The /var/log/httpd directory is where the Apache Web server’s log files (access logs and error logs) are located.
- /var/log/httpd 目录是 Apache Web 服务器日志文件（访问日志和错误日志）所在的位置。
- The /etc/rc.d/init.d/httpd script starts the httpd process as your Red Hat Linux system boots.
- /etc/rc.d/init.d/httpd 脚本在 Red Hat Linux 系统启动时启动 httpd 进程。

## Setting Up the FTP Server

## 设置 FTP 服务器

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_193_0.png)

Besides e-mail and Web, anonymous FTP is a common service on an Internet host. You may be familiar with FTP, which you can use to transfer files from one system to another on the Internet. When you use FTP to transfer files to or from a remote system, you have to log in to the remote system before you can use FTP.

除了电子邮件和 Web 之外，匿名 FTP 是 Internet 主机上的常见服务。您可能熟悉 FTP，您可以使用它在 Internet 上从一个系统向另一个系统传输文件。当您使用 FTP 向远程系统传输文件或从远程系统传输文件时，您必须先登录到远程系统，然后才能使用 FTP。

If you install Red Hat Linux from this book’s companion CD-ROMs, you should have anonymous FTP set up on your system and the FTP server configured to run when needed. The default setup also employs the necessary security precautions.

如果您从本书附带的 CD-ROM 安装 Red Hat Linux，您应该已在系统上设置了匿名 FTP，并且 FTP 服务器配置为在需要时运行。默认设置还采用了必要的
