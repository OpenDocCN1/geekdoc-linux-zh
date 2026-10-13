Sometimes data transfers can stall for various reasons, such as an overloaded server. While the default timeout is 300 seconds, the following commented directive suggests a shorter period:

```
#data_connection_timeout=120
```

The default nonprivileged user is named nobody, which does exist in the standard user authentication database. If you change the directive as suggested here, make sure the noted user actually exists in the authentication database.

```
#nopriv_user=ftpsecure
```

Some FTP clients may require the use of this feature to abort requests such as big file transfers. It's disabled by default:

```
#async_abor_enable=YES
```

Further down in the file is one other option associated with certain FTP clients, associated with recursive file lists. If you're configuring an FTP server for such clients, consider enabling the following directive:

```
#ls_recurse_enable=YES
```

As ASCII transfers to FTP servers are a known security risk, they are disabled by default. The following commented directives make it possible to enable such transfers:

```
#ascii_upload_enable=YES
#ascii_download_enable=YES
```

The first FTP servers were developed in a world where most Internet users could be trusted. Users who logged in anonymously were asked to supply their e-mail addresses as the password. An early security measure denied access to users who supplied e-mail addresses listed in the associated banned_email file:

```
#deny_email_enable=YES
#banned_email_file=/etc/vsftpd/banned_emails
```

The following two directives are important for vsFTP, especially on a network where both IPv4 and IPv6 networks have been enabled. First, one of these directives should be enabled to allow the control of vsFTP from the vsftpd script in the /etc/init.d directory. Second, both parameters can't be activated on the same vsFTP server. In other words, vsFTP can't communicate on both IPv4 and IPv6 networks simultaneously.

```
listen=YES
#listen_ipv6=YES
```