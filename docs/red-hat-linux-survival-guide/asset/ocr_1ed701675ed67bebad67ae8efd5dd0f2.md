```
server_args			= -l -a
```

To set a default umask for all files uploaded via FTP, you need to add a -u argument with the appropriate umask value. For example, to set 640 (rw-r-----) permission for each file uploaded, you can set the umask to 026. To do so, change the preceding line as follows:

```
server_args			= -l -a -u026
```

Then restart the inetd server (killall -USR1 xinetd) and FTP a file via a user account to see whether the permissions have been set as expected. This can be very handy for systems that act as Web servers for many different clients. If you do not want one client to see another client’s files, you can use this option along with a special ownership setting. For example, suppose you keep all of your Web client files in the /www partition or directory, where each client site has a directory of its own (for example, /www/myclient1, /www/myclient2, and so on). You have probably already given each client an FTP account with which to upload files to these directories. To stop a client from seeing another client’s files, use umask with the FTP server as described above and then reset the ownership of each client site as follows:

```
chown -R client.Web server user /www/client dir
```

For example, if you run your Web server as httpd and have a client user called myclient, then the preceding command will look like this:

```
chown -R myclient.httpd /www/myclient
```

This changes the ownership of the /www/myclient directory along with all of its subdirectories and files to the myclient user and to the httpd group, allowing the client user to own, modify, and delete her files and the Web server to read the files in the directory. To disallow everyone else, you must change the permissions as follows:

```
chmod -R 2770 /www/client dir
```

For the current example, the actual command is as follows:

```
chmod -R 2770 /www/myclient
```