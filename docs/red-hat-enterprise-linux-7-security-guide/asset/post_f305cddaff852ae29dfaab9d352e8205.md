
## 4.3.8.1. Securing Apache HTTP Server

System administrators should be careful when using the following configuration options (configured in `/etc/httpd/conf/httpd.conf`):

### FollowSymlinks

This directive is enabled by default, so be sure to use caution when creating symbolic links to the document root of the Web server. For instance, it is a bad idea to provide a symbolic link to `/.`

```bash
chmod 755 <directory_name>
```

### Indexes

This directive is enabled by default, but may not be desirable. To prevent visitors from browsing files on the server, remove this directive.

### UserDir

The `UserDir` directive is disabled by default because it can confirm the presence of a user account on the system. To enable user directory browsing on the server, use the following directives:

```apache
UserDir enabled
UserDir disabled root
```

These directives activate user directory browsing for all user directories other than `/root/`. To add users to the list of disabled accounts, add a space-delimited list of users on the `UserDir disabled` line.

### ServerTokens

The `ServerTokens` directive controls the server response header field which is sent back to clients. It includes various information which can be customized using the following parameters:

- **ServerTokens Full** (default option) – provides all available information (OS type and used modules), for example:

```text
Apache/2.0.41 (Unix) PHP/4.2.2 MyMod/1.2
```

- **ServerTokens Prod** or **ServerTokens ProductOnly** – provides the following information:

```text
Apache
```

- **ServerTokens Major** – provides the following information:

```text
Apache/2
```

- **ServerTokens Minor** – provides the following information:

```text
Apache/2.0
```

- **ServerTokens Min** or **ServerTokens Minimal** – provides the following information:

```text
Apache/2.0.41
```

- **ServerTokens OS** – provides the following information:

```text
Apache/2.0.41 (Unix)
```

It is recommended to use the **ServerTokens Prod** option so that a possible attacker does not gain any valuable information about your system.

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_55_0.png)

#### IMPORTANT

Do not remove the **IncludeNoExec** directive. By default, the **Server-Side Includes (SSI)** module cannot execute commands. It is recommended that you do not change this setting unless absolutely necessary, as it could, potentially, enable an attacker to execute commands on the system.

### Removing httpd Modules

In certain scenarios, it is beneficial to remove certain **httpd** modules to limit the functionality of the HTTP Server. To do so, edit configuration files in the `/etc/httpd/conf.modules.d` directory. For example, to remove the proxy module:

```bash
echo '# All proxy modules disabled' > /etc/httpd/conf.modules.d/00-proxy.conf
```

Note that the `/etc/httpd/conf.d/` directory contains configuration files which are used to load modules as well.

### httpd and SELinux

For information, see the *The Apache HTTP Server and SELinux* chapter from the *Red Hat Enterprise Linux 7 SELinux User's and Administrator's Guide*.

## 4.3.8.2. Securing NGINX

NGINX is a high-performance HTTP and proxy server. This section briefly documents additional steps that harden your NGINX configuration. Perform all of the following configuration changes in the **server** section of your NGINX configuration files.

### Disabling Version Strings

To prevent attackers from learning the version of NGINX running on your server, use the following configuration option:

```nginx
server_tokens    off;
```

This has the effect of removing the version number and simply reporting the string **nginx** in all requests served by NGINX:

```bash
$ curl -sI http://localhost | grep Server
Server: nginx
```

### Including Additional Security-Related Headers

Each request served by NGINX can include additional HTTP headers that mitigate certain known web application vulnerabilities:

- **add_header X-Frame-Options SAMEORIGIN;** – this option denies any page outside of your domain to frame any content served by NGINX, effectively mitigating clickjacking attacks.
- **add_header X-Content-Type-Options nosniff;** – this option prevents MIME-type sniffing in certain older browsers.
- **add_header X-XSS-Protection "1; mode=block";** – this option enables the Cross-Site Scripting (XSS) filtering, which prevents a browser from rendering potentially malicious content included in a response by NGINX.

### Disabling Potentially Harmful HTTP Methods

If enabled, some of the HTTP methods may allow an attacker to perform actions on the web server that were designed for developers to test web applications. For example, the TRACE method is known to allow Cross-Site Tracing (XST).

Your NGINX server can disallow these harmful HTTP methods as well as any arbitrary methods by whitelisting only those that should be allowed. For example:

```nginx
# Allow GET, PUT, POST; return "405 Method Not Allowed" for all others.
if ( $request_method !~ ^(GET|PUT|POST)$ ) {
    return 405;
}
```

### Configuring SSL

To protect the data served by your NGINX web server, consider serving it over HTTPS only. To generate a secure configuration profile for enabling SSL in your NGINX server, see the Mozilla SSL Configuration Generator. The generated configuration assures that known vulnerable protocols (for example, SSLv2 or SSLv3), ciphers, and hashing algorithms (for example, 3DES or MD5) are disabled.

You can also use the SSL Server Test to verify that your configuration meets modern security requirements.

## 4.3.9. Securing FTP

The File Transfer Protocol (FTP) is an older TCP protocol designed to transfer files over a network. Because all transactions with the server, including user authentication, are unencrypted, it is considered an insecure protocol and should be carefully configured.

Red Hat Enterprise Linux 7 provides two FTP servers:

- **Red Hat Content Accelerator (tux)** – A kernel-space Web server with FTP capabilities.
- **vsftpd** – A standalone, security oriented implementation of the FTP service.

The following security guidelines are for setting up the vsftpd FTP service.

### 4.3.9.1. FTP Greeting Banner

Before submitting a user name and password, all users are presented with a greeting banner. By default, this banner includes version information useful to crackers trying to identify weaknesses in a system.

To change the greeting banner for vsftpd, add the following directive to the `/etc/vsftpd/vsftpd.conf` file:

```ini
ftpd_banner=<insert_greeting_here>
```

Replace `<insert_greeting_here>` in the above directive with the text of the greeting message.

For multi-line banners, it is best to use a banner file. To simplify management of multiple banners, place all banners in a new directory called `/etc/banners/`. The banner file for FTP connections in this example is `/etc/banners/ftp.msg`. Below is an example of what such a file may look like:

```text
##########  Hello, all activity on ftp.example.com is logged.  ##########
```

#### NOTE

It is not necessary to begin each line of the file with 220 as specified in Section 4.4.1, “Securing Services With TCP Wrappers and xinetd”.

To reference this greeting banner file for vsftpd, add the following directive to the `/etc/vsftpd/vsftpd.conf` file:

```ini
banner_file=/etc/banners/ftp.msg
```

It also is possible to send additional banners to incoming connections using TCP Wrappers as described in Section 4.4.1, “TCP Wrappers and Connection Banners”.

### 4.3.9.2. Anonymous Access

The presence of the `/var/ftp/` directory activates the anonymous account.

The easiest way to create this directory is to install the vsftpd package. This package establishes a directory tree for anonymous users and configures the permissions on directories to read-only for anonymous users.

By default the anonymous user cannot write to any directories.

#### WARNING

If enabling anonymous access to an FTP server, be aware of where sensitive data is stored.

### 4.3.9.2.1. Anonymous Upload

To allow anonymous users to upload files, it is recommended that a write-only directory be created within `/var/ftp/pub/`. To do this, enter the following command as root:

```bash
[~]# mkdir /var/ftp/pub/upload
```

Next, change the permissions so that anonymous users cannot view the contents of the directory:
