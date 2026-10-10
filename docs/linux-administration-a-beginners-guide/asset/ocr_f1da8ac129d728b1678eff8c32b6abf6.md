days of the week for all day. (Real users who try to log in are sent the content of the file /home//ftp/.norealeusers.) The rest of the file is pretty generic; you’ll see it in many different configurations.

# ## Setting Up an Incoming Directory

If you need to allow anonymous users to deposit files onto your system, you will need to set up a special incoming directory for them. Files placed there can be retrieved only by the root user, not by other anonymous users. This is so that individuals with dishonorable intentions don’t turn your FTP server into a public access site for their stash of pornography, pirated software, or illegal content (such as stolen credit card numbers). This of course means there are overhead for you as a site administrator, but a human safety shield is the only way you can ensure that anonymously uploaded files are acceptable for keeping on the server for others to download.

To create this directory, go to your anonymous FTP directory (for example, /home//ftp) and create a subdirectory called “incoming,” like so:

```
mkdir incoming
```

Then change the permissions so that only the user ftp can write to it, but the anonymous user cannot read from it:

```
chmod 300 incoming
chown ftp.ftp incoming
```

And lastly, add the following two lines to your /etc/ftpgaccess file to control where uploads go:

```
upload /home/ftp * no
upload /home/ftp/incoming yes ftp ftp 0000 nondos
```

The first upload command denies uploading to all directories on your FTP server. The second command then explicitly opens up one directory where anonymous users can upload files.

# ## Registered Users Only and Mixed Access

It is entirely acceptable to run a server that supports mixed access; that is, it provides both anonymous users and regular users access to the server. It is also possible to configure a server with only registered users access.

# ### Mixed Access

Begin by configuring the server as you would for anonymous-only access. Once set up, change the /etc/ftpgaccess file so that it reads

```
class all real,quest,anonymous *
class ftp@admin.com
```