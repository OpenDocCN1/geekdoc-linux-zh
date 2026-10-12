With ftpshut command, you can either shut down the server immediately or set it to shut down some time in the future. When you run ftpshut, it creates a shutdown file. To restart the FTP service after it has been shut down, you need to remove that file.

The ftpshut command shuts down the FTP service. Any users who are currently connected to the FTP service are disconnected. When they type FTP commands, they will see a message such as “FTP server shut down — please try again later” or simply “Not connected.” To shut down the service immediately, type the following:

```
```text
# ftpshut now
```
```

You can set the server to shut down at a specific time by either adding the number of minutes from now that you want the server to shut down or by entering a particular time in the future. Here are some examples:

```
```text
# ftpshut 20:18
# ftpshut -1 20 -d 3
```
```

In the first example, the server is set to shut down at 20:18 (or 8:18 p.m. on a 12-hour clock). In the second example, the -1 option specifies the number of minutes left before the server will be shut down (in this example, 20 minutes). The -d option specifies the number of minutes before the FTP service shuts down that users are disconnected from the server. (If no -d option is specified, users are disconnected five minutes before the server shuts down.)

To be less antisocial about shutting down your FTP service, it’s nice to send a warning message to let users know that FTP is going down. Here’s an example of how to send a shutdown-warning message when you shut down your FTP server:

```
```text
ftpshut 20:15 "FTP will go down soon. Finish and disconnect."
```
```

# ### Restarting FTP

After ftpshut is run, it creates a file called shutmsg in both the /etc and /var/ftp/etc directories. When your FTP server shuts down, it stays down until these files are removed. So, to restart your FTP server, all you have to do is the following (as root user):

```
```text
# rm /etc/shutmsg /var/ftp/etc/shutmsg
```
```

The above command removes the files. At this point, users will immediately be able to reconnect to your FTP server. Another command you could use to restart your FTP server is the ftprestart command.

# ## Monitoring the WU-FTP server

Whenever you set up a service from your computer for general consumption, it’s a good idea to keep an eye on it. You can use many of the same techniques that you use to monitor your computer’s file system in general to monitor your FTP server (for example, various tools for