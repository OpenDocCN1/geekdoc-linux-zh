+   4. Uncomment the directory section defined for the home directory to control access to UserDir directories.

```apache
<Directory /home/user_name/public_html>
  AllowOverride FileInfo AuthConfig Limit
  Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec
  <Limit GET POST OPTIONS>
    Order allow,deny
    Allow from all
  </Limit>
  <LimitExcept GET POST OPTIONS>
    Order deny,allow
    Deny from all
  </LimitExcept>
</Directory>
```

+   5. Save and close the file.

6. Enter `mkdir /home/user_name/public_html` to create a directory for the web content.

7. Copy the user's own web content into `/home/{user name}/public_html`.

8. Enter `chown -R user_name:User_group /home/user_name` to change the ownership permission of the user's home directory.

9. Enter `chmod -R 755 /home/user_name` to change the permissions of the user's home directory.

10. Enter `service httpd configtest` to test the configuration file.

11. Enter `service httpd restart` to restart the httpd service for the configuration changes to take effect.

12. Access the website and verify the configuration.
    `http://localhost/~user_name`

# Procedure Reference: Configure the Apache Log

To configure the Apache log:

+   1. Log in as root.

2. Using the vi editor, open the `/etc/httpd/conf/httpd.conf` file.

3. Locate the `ErrorLog` statement and specify the location where error logs should be stored.
   `ErrorLog (location of error logs)`

4. Locate and specify the `CustomLog` directive.
   a. Specify a log format by using the `LogFormat` directive.
   `LogFormat "format" format_name`
   b. Define a `CustomLog` directive that uses the log format you created.
   `CustomLog logs/access_log format_name`

![](bbox=[0.32, 0.85, 0.98, 0.92])