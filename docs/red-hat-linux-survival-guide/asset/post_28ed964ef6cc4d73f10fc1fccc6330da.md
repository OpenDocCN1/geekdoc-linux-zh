
ratecard.html.bak, or ratecard.bak, ratecard.old, etc., if ratecard.html is missing. This may or may not be desirable, depending on your needs.

- No options specified here can be overridden by a local access control file (specified by the AccessFileName directive in httpd.conf; the default is .htaccess). This is specified using the AllowOverride directive.
- The Allow directives are evaluated before the Deny directives. Access is denied by default. Any client that does not match an Allow directive or does match a Deny directive will be denied access to the server.
- Access is permitted for all.

The default settings for these directives should be sufficient.

![](img/9eb7e89292d2f85707b4d49102c865b7_327_0.png)

If your server is going to be on the Internet, you may want to remove the FollowSymLinks option from the Options directive line. Leaving this option creates a potential security risk. For example, if a directory in your Web site does not have an index page, the server displays an automated index that shows any symbolic links you may have in that directory. This could result in sensitive information being inadvertently displayed to Web surfers, or allow anyone to run an executable that resides in a carelessly linked directory.

## UserDir

The UserDir directive tells Apache to consider UserDir as document root (~username/UserDir) of each user of the Web site. This only makes sense if you have multiple users on the system and want to allow each one to have his very own Web directory. The default setting is

```
UserDir public_html
```

which means that if you set up your Web server's name to be www.company.com, and you have two users (say joe and bob) their personal Web site URLs would be as shown:

```
http://www.company.com/~joe Physical directory: ~joe/public_html
http://www.company.com/~bob Physical directory: ~bob/public_html
```

Note that on Red Hat Linux systems, ~ (tilde) expands to a user's home directory. The directory specified by the UserDir directive resides in each user's home directory, and Apache must have read and execute permissions to read files and directories within the public_html directory. This can be accomplished using the following commands on a Red Hat Linux system:

```
chown -R user.Apache_server_group ~user/dir_assigned_in_UserDir
chmod -R 770 ~user/dir_assigned_in_UserDir
```

For example, if the user name is joe and Apache's group is called httpd, and public_html is assigned in the UserDir directive, the preceding commands will look like this:

```
chown -R joe.httpd ~joe/public_html
chmod -R 2770 ~joe/public_html
```

The first command, chown, gives user joe and the group httpd full ownership of all the files and directories in the public_html directory. The next command, chmod, sets the access rights to 2770 (that is, only the user joe and the group httpd have full read, write, and execute privileges in public_html and all files and subdirectories under it. This also ensures that when a new file or subdirectory is created in the public_html directory, the newly created file has the group ID set, which enables the Web server to access the new file without the user's intervention.

If you create user accounts on your system by using a script (such as /usr/sbin/adduser script on Linux systems), you may want to incorporate the Web site creation process in this script. Just add a mkdir command to create a default public_html directory (if that's what you assign to the UserDir directive) to create the Web directory. Add the chmod and chown commands to give the Web server user permission to read and execute files and directories under this public directory.

## DirectoryIndex

Next, you need to configure the DirectoryIndex directive, which has the following syntax:

```
DirectoryIndex [filename1, filename2, filename3, ... ]
```

This directive specifies which file the Apache server should consider as the index for the directory being requested. For example, when a URL such as www.yourcompany.com/ is requested, the Apache server determines

that this is a request to access the / (document root) directory of the Web site. If the DocumentRoot directive is set as follows

```
DocumentRoot "/www/www.yourcompany.com/public/htdocs"
```

then the Apache server looks for a file named /www/www.yourcompany.com/public/htdocs/index.html; if it finds the file, Apache services the request by returning the content of the file to the requesting Web browser. If the DirectoryIndex is assigned welcome.html instead of the default index.html, however, the Web server will look for the following site instead:

```
/www/www.yourcompany.com/public/htdocs/welcome.html
```

If the file is absent, Apache returns the directory listing by creating a dynamic HTML page.

You can specify multiple index filenames in the DirectoryIndex directive. For example:

```
DirectoryIndex index.html index.htm welcome.htm
```

tells the Web server that it should check for the existence of any of the three files, and that if any one is found, it should be returned to the requesting Web client.

## AccessFileName

The AccessFileName directive defines the name of the per-directory access control configuration file. The default name, .htaccess, has a leading period to hide the file from normal directory listing. The only reason to change the name to something else is to increase security by using an obscure name, which is not much of a security benefit. However, if you do change the filename to something else make sure you change the regular expression ^\.ht to ^\.whatever where .whatever is the first character of what you set AccessFileName to.

The following <Files ...> container tells Apache to disallow access to any file that starts with a .ht (e.g. .htaccess or .htpasswd). This corresponds to the default AccessFileName.

```
<Files "~^\\.ht">
    Order allow,deny
    Deny from all
</Files>
```

## UseCanonicalName

UseCanonicalName, which is typically set to On, tells Apache to create all self-referencing URLs using ServerName:Port format. Leaving it on is a good idea.

## TypesConfig

The TypesConfig directive points to the MIME configuration file mime.types that resides in the default conf directory. You do not need to change this directive unless you have relocated this file somewhere else.

## DefaultType

The DefaultType directive sets the Content-Type header for any file whose MIME type cannot be determined from the file extension. For example if you have a file DocumentRoot/myfile, Apache uses the DefaultType setting, which is text/plain, as the content type for the file. This means that when the Web browser requests and receives such a file in response, it displays the contents in the same way that it displays a plain-text file. But, for example, if you think that most of your unknown file contents should be treated as HTML you can use text/html in place of text/plain.

The next <IfModule ...> container tells Apache to enable the MIME magic module (mod_mime_magic) if it exists and to use the MIMEMagicFile as the magic information (bytes patterns) needed to identify MIME type of files. The default should be left alone unless you want to change the path of the magic file.

```
<IfModule mod_mime_magic.c>
    MIMEMagicFile conf/magic
</IfModule>
```

### HostnameLookups

The HostnameLookups directive tells Apache to enable DNS lookup per request if this directive is set to On. However, the default setting is Off and therefore no DNS lookup is performed to process a request, which speeds up response time. Performing a DNS lookup to resolve IP address to hostname is a time-consuming step for a busy server and should only be done using the logresolve utility. Leave the default as is.

## ErrorLog

The ErrorLog directive is very important; it points to the log file that is dedicated to recording server errors. The default value of logs/errors translates to ServerRoot/logs/error_log, which should work unless you want to write a log in a different place. Generally it’s a good idea to create a log partition where you can keep your logs; it’s also preferable that your log partition is on one or more dedicated log disks. If you have such a hardware configuration you might want to change the directive to point to a new log path.

## LogLevel

The LogLevel directive sets the level of logging that will be done. The default value of warn is sufficient for getting started. The LogFormat directives dictate what is logged and in what format. The CustomLog directive sets the path for the access log, which stores your server hits. By default it uses the common (CLF) format that is defined in a LogFormat directive, which is discussed in the “Creating log files” section below. Consider the advice about keeping logs on their own disk and partition and then make changes to the path if necessary.

![](img/9eb7e89292d2f85707b4d49102c865b7_331_0.png)

> Some common advice for all logs: Whatever directory you keep logs in, make sure that only the primary server process has write access in that directory. This is a major security issue, because allowing other users or processes to write to the log directory can allow someone unauthorized to take over your primary Web server process UID, which is normally the root account.

## ServerSignature

The ServerSignature directive displays the server name and the server’s version number in a server-generated page such as dynamic directory index pages, error pages, etc. If you feel uncomfortable about displaying your server information so readily to everyone, set it to Off. I do.

## Alias

The Alias directive defines a new directory alias called /icons/ to point to /usr/local/apache/icons/ (i.e., ServerRoot/icons/). The icon
