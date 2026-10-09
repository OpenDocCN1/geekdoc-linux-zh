
## Domain Configuration for www.vhost1.com

```apache
<VirtualHost www.vhost1.com>
    ServerName www.vhost1.com
    ServerAdmin webmaster@vhost1.com
    DocumentRoot /tmp/vhost1/htdocs
    ScriptAlias /cgi-bin/ /tmp/vhost1/cgi-bin/
    ErrorLog logs/www.vhost1.com.error.log
    TransferLog logs/www.vhost1.com.access.log
</VirtualHost>
```

This is the `<VirtualHost>` configuration that the makesite script creates.

> **Tip** | If you are creating a name-virtual host for the first time, make sure you add `NameVirtualHost IP_Address` as the last line in the `httpd.conf` file before running makesite script for the first time.

Also check the `/etc/named.conf` file; you should see the following:

```bind
// vhost1.com was created on 2001-04-25-17-25
zone "vhost1.com" {
    type master;
    file "vhost1.zone";
};
```

As you can see, the script created the appropriate zone configuration information for the virtual host. You can find the DNS zone information in `/var/named/vhost1.zone` file, which shows:

```dns
@       IN  SOA vhost1.com. hostmaster.vhost1.com. (
                20010425000         ; serial YYYYMMDDXXX
                7200                ; refresh
                3600                ; (1 hour) retry
                1728000             ; (20 days) expire
                3600)              ; (1 hour) minimal TTL
: Name Servers
IN  NS  ns1.domain.com.
IN  NS  ns2.domain.com.
IN  MX  10 mail.domain.com.
: CNAME records
www   IN  CNAME  www.domain.com.
```

Look under `/www` (or whatever `$BASE_DIR` is pointing to); you should see `vhost1` directory with the following files and subdirectories:

- `./vhost1`
- `./vhost1/htdocs`
- `./vhost1/htdocs/index.html`
- `./vhost1/cgi-bin`

Restart the name server by using the `killall -HUP named` command. Also restart the Apache server by using the `/usr/local/apache/bin/apachectl restart` command. You should be able to access the new virtual Web site by using `www.vhost1.com/`. The default `index.html` page is there to help you identify the domain via Web.

### Managing Virtual Hosts By Using MySQL with mod_v2h Module

The `mod_v2h` module is a mass virtual-hosting module with support for performing URL translation paths from MySQL database. This module can cache URL translation paths into memory for faster performance. You will need to have MySQL installed on a server. To learn about MySQL visit `www.mysql.com`.

With MySQL already installed, follow these steps to compile and install `mod_v2h`:

1.  Download the latest version of `mod_v2h` from `www.fractal.net/mod_v2h.tm`.
2.  As root, extract the source distribution using the `tar xVZF mod_v2h.tar.gz` command in the modules subdirectory of your Apache source tree. For example, if you keep the Apache source in `/usr/local/src/httpd_2_0_16` directory, then extract the `mod_v2h.tar.gz` file in the `/usr/local/src/httpd_2_0_16/modules` directory. A new subdirectory called `mod_v2h` will be created.
3.  Change your current directory to `/usr/local/src/httpd_2_0_16/modules/v2h` and edit the `config.m4` file.

You only need to edit this file if you notice that the `include` and `lib` directory path for MySQL files are incorrect. For example, on my Linux system, the MySQL include files are installed in `/usr/include/mysql` directory and the library files are in `/usr/lib/mysql` directory. The default `config.m4` points to `/usr/local/include/mysql` and `/usr/local/lib/mysql` for the include and library files, respectively; thus, I had to correct the path. Simply edit the path if needed. I also needed to add `-lz` in the LDFLAGS line so that it looked like `LDFLAGS="*$LDFLAGS -L/usr/lib/mysql -lz -Wl,-R,/usr/lib/mysql*".`

4.  Change directory to `/usr/local/src/httpd_2_0_16` and run the autoconf command to create necessary configuration file.
5.  Run `./configure` with whatever options you need as shown in Chapter 2 and then run `make && make install` commands to compile and install Apache with `mod_v2h` support. For example, I ran `./configure --prefix=/usr/local/httpd --disable-module=cgi` to configure Apache source and then ran the `make && make install` commands to install Apache in `/usr/local/httpd` with `mod_v2h` support and without `mod_cgi` support. (You can use whatever options you used earlier by not running `./configure` and by running `./config.status` instead.)

After you have compiled Apache with `mod_v2h`, you need to use the new `mod_v2h` directives, which are shown in Table 6-2, in `httpd.conf`.

**Table 6-2 The mod_v2h directives**

# Chapter 7
# Authenticating and Authorizing Web Site Visitors

## In This Chapter

- Authenticating users by using usernames and passwords
- Authorizing access using host name or IP address
- Authenticating with RDBM
- Authenticating using MySQL Database
- Authenticating using the `/etc/passwd` password file
- Authenticating using cookies

Support for basic HTTP authentication in Apache has been around for quite a while. Many modules have been written to provide basic HTTP authentication in Apache. In this chapter you will learn about various ways of authenticating and authorizing access to the Web server, how you can authenticate users using password files, database servers, etc., and how to control access by restricting access via IP address or usernames.

## Authentication vs. Authorization

Many people confuse authentication and authorization, and some even think they are the same thing, which they aren't. To understand the differences consider the following example. When you want to visit a foreign country what do you need? A passport and a visa. The passport is a document that authenticates you to the foreign country. It tells them that you are really who you claim to be. So, when you present your passport, you are authenticating yourself to the foreign officials. Next, you must show proof that you are allowed (that is, authorized) to enter the foreign country. This is the visa document.

Now, in computer terms, the *authentication* typically involves submitting a username and password. A successful submission and acceptance of a username and password states that you are who you claim to be. In other words, you have *authenticated* yourself.

A given resource that you are trying to access may require authorization in addition to authentication. For example, if you are accessing a computer at 4 a.m., the computer might refuse to let you in at that time because the system administrator has decided that you are not authorized to access it at 4 a.m. Similarly, you might be authorized to view a restricted Web site from the office but not from home because the company policy dictates to the network administrator that all restricted access be performed on premises.

### Understanding How Authentication Works

Basic HTTP authentication is really quite simple. A challenge and response mechanism is used to authenticate users. The steps are shown in Figure 7-1 and discussed below:

1.  Authentication begins when a Web browser requests a URL that is protected by the HTTP authentication scheme. This is shown as (1) in the figure.
2.  The Web server then returns a 401 status header along with a WWW-Authenticate response header, which implies that authentication is required to access the URL. The header contains the authentication scheme being used (currently only basic HTTP authentication is supported) and the realm name. This is (2) in the figure.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_212_0.png)

3.  At this point, a Web browser dialog box appears, asking the user to enter a username and a password. This is (3) in the figure.
4.  The user enters the required username and password and clicks OK. The browser then sends the username and password along with the previous URL request to the server. The server checks whether the username and password are valid. This is (4) in the figure.

> **Caution**
>
> When the password is sent from the client system (the host running the Web browser), it is neither sent in clear text nor encrypted. Instead, it is uuencoded and transmitted over the Internet. This is disadvantageous for this method of authentication, because anyone armed with network traffic sniffer hardware and software might be able to retrieve the IP packet carrying the uuencoded password. Because uuencode is a widely used data-encoding scheme, the decoder, uudecode, is also widely available, thus enabling practically anyone to decode a uuencoded password and to possibly abuse it. It is true that the packet sniffer has to be able to find the right packet to be able to do the decoding, but technically it is possible. This is why you should never use Basic HTTP authentication for any critical application. Do not, for example, protect your nation’s secrets using this scheme. However, if you are already allowing Telnet or ftp access to your system, then you are already using authentication methods (in these services) that are very similar to Basic HTTP authentication. If you trust your server to be connected to the Internet, open to attempts to Telnet in by anyone who wants to try, then you have no reason not to trust this method.

5.  If the username and password are valid (that is, authentic), the server returns the requested page. This is (5a) in the figure. If the username and password are invalid, the server responds with a 401 status and sends the same WWW-Authenticate response header to the browser. This is (5b) in the figure.
6.  In each subsequent request during the browser session to the same server, the browser will send the username and password pair so that the server does not have to generate a 401 status header for calls that fall in the same area of the site. For example, if the URL `/apache.nitcc.com/protected/` requires Basic HTTP authentication, subsequent calls to `http://apache.nitcc.com/protected/a=page.html` and `http://apache.nitcc.com/protected/b=page` also require the username and password. This is why the browser sends both before another authentication challenge—that is, the 401 status header and the WWW-Authenticate response header—is issued by the server. This is faster and more practical than generating a challenge for each request and having the user enter the username and password repeatedly.
