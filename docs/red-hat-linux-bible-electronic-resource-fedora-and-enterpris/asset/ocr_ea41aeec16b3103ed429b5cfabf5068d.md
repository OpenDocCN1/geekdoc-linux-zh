# # Setting timeouts

The following timeouts are set by default in vsFTPd (these values are built-in, so you don’t have to make any changes to the `/etc/vsftpd/vsftpd.conf` file for them to take effect):

```
```text
accept_timeout=60
connect_timeout=60
idle_session_timeout=600
data_connection_timeout=120
```
```

The `accept_timeout=60` and `connect_timeout=60` values determine how long the client has to establish a PASV or PORT style connection, respectively, before the connection times out. Both are set to 60 seconds. The `idle_session_timeout=600` option causes the FTP session to be dropped if the user has been inactive for more than 10 minutes (600 seconds). The `data_connection_timeout` value sets the amount of time, during which no progress occurs, that the server will wait before dropping the connection (the default here is 120 seconds, or two minutes).

# ## Navigating the vsFTPd site

In general, vsFTPd does not offer as many shortcuts for clients trying to navigate through the FTP site as does WU-FTPD. For example, most shell wildcard characters that a user might expect to use, such as question marks and brackets, are not supported.

There is, however, one very useful wildcard character you can use with the `ls` command, and one option you can turn. The asterisk (*) wildcard can be used with the `ls` command. Multiple asterisks in the same line are supported. You can add support for the `-R` option of `ls` so that a user can recursively list the contents of the current directory and all subdirectories. To turn on this feature, which is off by default, you can add the following line to the `vsftpd.conf` file:

```
```text
ls_recurse_enable=YES
```
```

# # Using the Washington University FTP Server (WU-FTPD)

Although WU-FTPD was dropped from the distribution, you can still use WU-FTPD by downloading and installing the following packages from `rpmfind.net`:

+   - anongftp-4.0-12.i386.rpm
+   - wu-ftpd-2.6.2-8.i386.rpm

When WU-FTPD is first installed, it is disabled. However, much of the FTP configuration is already in place.

> > **NOTE**: Refer to “Starting and shutting down the WU-FTPD service” to see how to start the FTP server.

The following sections describe the setup of the `wu-ftpd` package when it is first installed: