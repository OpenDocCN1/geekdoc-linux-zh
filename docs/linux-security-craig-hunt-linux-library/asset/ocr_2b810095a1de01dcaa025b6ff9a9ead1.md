Hiding Directory Contents By default, when the browser requests a directory listing in the URL, Apache returns the contents of one of the files listed under the `DirectoryIndex` directive, for example:

```
DirectoryIndex index.html index.htm index.shtml index.php index.php4 index.php3 index.cgi
```

However, if one of these files is temporarily unavailable, the user may actually get a listing of all the files on the directory, including script and header files that you may not want the user to be able to list. To prevent this, make sure that all content directories have their read bit turned off for group and other by executing the following commands:

```
[ramon]$ cd /var/www
[ramon]$ ls -ld html
drwxr-xr-x 2 apache apache 1024 Dec 4 20:44 html
[ramon]$ sudo -u apache chmod go-r html
[ramon]$ ls -ld html
drwx--x--x 2 apache apache 1024 Dec 4 20:44 html
```

CGI Scripts Common Gateway Interface (CGI) scripts allow your users to execute code in response to HTTP input and return something meaningful to the remote browser. As with any executable, make sure that your users are writing safe scripts and that the ownership and permissions of these scripts are correct. To accomplish this, Apache allows you to restrict all CGI scripts to a single directory using an httpd.conf directive like the following:

```
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/*"
```

This directive ensures that all CGI scripts live on the /var/www/cgi-bin directory, where you can easily track and monitor them. You should examine this directory periodically to ensure that there are no world-writable script files on it.

Server Side Includes Server side includes (SSIs) are extensions to the static HTML content that allow for conditional execution of external programs, as well as "just-in-time" content modification. SSIs represent a potential security problem, since it is difficult to put bounds on the programs that an HTML file is allowed to execute.