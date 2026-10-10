
```
DocumentRoot /srv/www.example.com/www
</VirtualHost>
```

You might also consider adding CustomLog and ErrorLog directives to configure Apache to output logs in files dedicated to the virtual host.

# *Common Directives*

This section briefly reviews some of the commonly-used Apache configuration directives. The main configuration file usually includes several Directory blocks; they allow specifying different behaviors for the server depending on the location of the file being served. Such a block commonly includes Options and AllowOverride directives:

```
<Directory /var/www>
Options Includes FollowSymlinks
AllowOverride All
DirectoryIndex index.php index.html index.htm
</Directory>
```

The DirectoryIndex directive contains a list of files to try when the client request matches a directory. The first existing file in the list is used and sent as a response.
The Options directive is followed by a list of options to enable. The None value disables all options; correspondingly, All enables them all except MultiViews. Available options include:

- ExecCGI—indicates that CGI scripts can be executed.
- FollowSymlinks—tells the server that symbolic links can be followed, and that the response should contain the contents of the target of such links.
- SymLinksIfOwnerMatch—also tells the server to follow symbolic links, but only when the link and its target have the same owner.
- Includes—enables Server Side Includes (SSI). These are directives embedded in HTML pages and executed on the fly for each request.
- Indexes—tells the server to list the contents of a directory if the HTTP request sent by the client points to a directory without an index file (that is, when no files mentioned by the DirectoryIndex directive exist in this directory).
- MultiViews—enables content negotiation; this can be used by the server to return a web page matching the preferred language as configured in the browser.

# Requiring Authentication

In some circumstances, access to part of a website needs to be restricted, so only legitimate users who provide a username and a password are granted access to the contents.

The `.htaccess` file contains Apache configuration directives enforced each time a request concerns an element from the directory where the `.htaccess` file is stored. These directives are recursive, expanding the scope to all subdirectories.

Most of the directives that can occur in a Directory block are also legal in an .htaccess file. The AllowOverride directive lists all the options that can be enabled or disabled by way of .htaccess. A common use of this option is to restrict ExecCGI, so that the administrator chooses which users are allowed to run programs under the web server’s identity (the www-data user).

## Example 5.3 `.htaccess` File Requiring Authentication

```
Require valid-user
AuthName "Private directory"
AuthType Basic
AuthUserFile /etc/apache2/authfiles/htpasswd-private
```

| **Basic Authentication Offers No Security** | The authentication system used in the above example (Basic) has minimal security as the password is sent in clear text (it is only encoded as base64, which is a simple encoding rather than an encryption method). It should also be noted that the documents protected by this mechanism also go over the network in the clear. If security is important, the entire HTTP session should be encrypted with Transport Layer Security (TLS). |
|---|---|

The /etc/apache2/authfiles/htpasswd-private file contains a list of users and passwords; it is commonly manipulated with the htpasswd command. For example, the following command is used to add a user or change their password:

```
# htpasswd /etc/apache2/authfiles/htpasswd-private user
New password:
Re-type new password:
Adding password for user user
```

# Restricting Access

The Require directive controls access restrictions for a directory (and its subdirectories, recursively).

It can be used to restrict access based on many criteria; we will stop at describing access restriction based on the IP address of the client but it can be made much more powerful than that, especially when several Require directives are combined within a RequireAll block.

For instance, you could restrict access to the local network with the following directive:

```
Require ip 192.168.0.0/16
```

## 5.4. Managing Services

Kali uses `systemd` as its init system, which is not only responsible for the boot sequence, but also permanently acts as a full featured service manager, starting and monitoring services. `systemd` can be queried and controlled with `systemctl`. Without any argument, it runs the `systemctl list-units` command, which outputs a list of the active units. If you run `systemctl status`, the output shows a hierarchcal overview of the running services. Comparing both outputs, you immediately see that there are multiple kinds of units and that services are only one among them.

Each service is represented by a *service unit*, which is described by a service file usually shipped in `/lib/systemd/system/` (or `/run/systemd/system/`, or `/etc/systemd/system/`; they are listed by increasing order of importance, and the last one wins). Each is possibly modified by other `service-name.service.d/*.conf` files in the same set of directories. Those unit files are plain text files whose format is inspired by the well-known `*.ini` files of Microsoft Windows, with `key = value` pairs grouped between `[section]` headers. Here we see a sample service file for `/lib/systemd/system/ssh.service`:

```
[Unit]
Description=OpenBSD Secure Shell server
After=network.target auditd.service
ConditionPathExists=!/etc/ssh/sshd_not_to_be_run

[Service]
EnvironmentFile=-/etc/default/ssh
ExecStart=/usr/sbin/sshd -D $SSH_OPTS
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Restart=on-failure
RestartPreventExitStatus=255
Type=notify

[Install]
WantedBy=multi-user.target
Alias=sshd.service
```

Target units are another part of systemd’s design. They represent a desired state that you want to attain in terms of activated units (which means a running service in the case of service units). They exist mainly as a way to group dependencies on other units. When the system starts, it enables the units required to reach the `default.target` (which is a symlink to `graphical.target`, and which in turn depends on `multi-user.target`). So all the dependencies of those targets get activated during boot.

Such dependencies are expressed with the `Wants` directive on the target unit. But you don’t have to edit the target unit to add new dependencies, you can also create a symlink pointing to the dependent unit in the /etc/systemd/system/target-name.target.wants/ directory. And this is exactly what `systemctl enable foo.service` does. When you enable a service, you tell systemd to add a dependency on the targets listed in the WantedBy entry of the [Install] section of the service unit file. Conversely, `systemctl disable foo.service` drops the same symlink and thus the dependency.

The enable and disable commands do not change anything regarding the current status of the services. They only influence what will happen at next boot. If you want to run the service immediately, you should execute `systemctl start foo.service`. Conversely, you can stop it with `systemctl stop foo.service`. You can also inspect the current status of a service with `systemctl status foo.service`, which usefully includes the latest lines of the associated log. After having changed the configuration of a service, you may wish to reload it or restart it: those operations are done with `systemctl reload foo.service` and `systemctl restart foo.service` respectively.

```
# systemctl status postgresql
● postgresql.service - PostgreSQL RDBMS
   Loaded: loaded (/lib/systemd/system/postgresql.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
# ls -al /etc/systemd/system/multi-user.target.wants/postgresql.service
ls: cannot access ‘/etc/systemd/system/multi-user.target.wants/postgresql.service’: No such file or directory
# systemctl enable postgresql
[...]
# ls -al /etc/systemd/system/multi-user.target.wants/postgresql.service
lrwxrwxwx 1 root root 38 Apr 21 16:21 /etc/systemd/system/multi-user.target.wants/postgresql.service -> /lib/systemd/system/postgresql.service
# systemctl status postgresql
● postgresql.service - PostgreSQL RDBMS
   Loaded: loaded (/lib/systemd/system/postgresql.service; enabled; vendor preset: disabled)
   Active: inactive (dead)
# systemctl start postgresql
# systemctl status postgresql
● postgresql.service - PostgreSQL RDBMS
   Loaded: loaded (/lib/systemd/system/postgresql.service; enabled; vendor preset: disabled)
   Active: active (exited) since Thu 2016-04-21 16:22:29 EDT; 2s ago
   Process: 6355 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
 Main PID: 6355 (code=exited, status=0/SUCCESS)

Apr 21 16:22:29 kali-rolling systemd[1]: Starting PostgreSQL RDBMS...
Apr 21 16:22:29 kali-rolling systemd[1]: Started PostgreSQL RDBMS.
```
