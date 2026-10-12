# Testing Apache

After you have started the Apache server, access it via a Web browser by using the appropriate host name. For example, if you are running the Web browser on the server itself, than use http://localhost/ to access the server. However, if you want to access the server from a remote host, use the fully qualified host name of the server. For example to access a server called apache.pcnltd.com, use http://apache.pcnltd.com.

![](bbox=[0.08, 0.32, 0.18, 0.4])

> If you have set the Port directive to a non-standard port (i.e., not 80), don't forget to include the :port in the URL. For example, http://localhost:8080 will access Apache server on port 8080.

If you have not made any changes to the default htdocs directory, you'll see the default page that is shipped with the Apache distribution; this needs to be replaced with your own content.

Finally, you want to make sure the log files are updated properly. To check your log files, enter the log directory and run the following command:

```
tail -f /path/to/access_log
```

With the -f option specified, the tail utility lets you view a growing file. Now, use a Web browser to access the site, or if you are already there, simply reload the page you currently have on the browser. You should see an entry added to the listing on the screen. Press the Reload button a few more times to ensure the access file is updated accordingly. If you see the updated records, your access log file is working. Press Control+C to exit from the tail command session. If you don't see any new records in the file, you should check the permission settings for the log files and the directory in which they are kept.

Another log to check is the error log file. Use the following command to view the error log entries as they come in:

```
tail -f /path/to/error_log
```

Simply request nonexistent resources (such as a file you don't have) on your Web browser, and you will see entries being added. If you observe this, the error log file is properly configured.

If all of these tests were successful, then you have successfully configured your Apache server. Congratulations!