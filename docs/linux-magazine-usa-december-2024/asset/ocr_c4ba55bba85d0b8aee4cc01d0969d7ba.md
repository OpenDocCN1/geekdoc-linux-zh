of the database it should use. You've already created a database named `owncloud` and noted the password in the previous step. During this setup, you'll need to provide a username and password for the admin account that you also must remember.

I added a group called `regular` (via `admin/users/groups/add group`) and made a user called `user` with password `user` on the same user and group management page. By default, `ownCloud` asks for an email address to validate a new user, but you can click on the cog icon in the lower left corner and enable the Set password for new users option. That will replace the email address input field with a password field (Figure 3). As a minor tweak, I changed the prompt message in `/var/www/html/owncloud/core/templates/login.php` so that it asks for `Username` instead of `Username or email` (Figure 4).

`ownCloud` will only allow users from certain trusted domains. Since my domain is `lodge.local`, I added the file `/var/www/html/owncloud/core/config/config.php` that defines an array called `trusted_domains`.

# Setting Up the Web Server

With Apache installed, now it's time to customize it. First, enable the Apache

# What About HTTPS?

Do you want or need SSL/TLS? There are two possible uses: to intercept HTTPS requests to other websites and redirect them to your homepage, and to present your homepage with HTTPS. Here is the breakdown:

+   1. I tried setting up SSL/TLS on Apache to intercept HTTPS URLs, but my certificate didn't match and the browser correctly told the user so. There used to be a way for users to "accept the risk," but that isn't offered anymore. So now it will just confuse people.
+   2. Because I don't have a live connection, I cannot get a certificate from Let's Encrypt. So the only free option is a self-signed certificate. But browsers now complain about self-signed certificates, so HTTPS for my homepage doesn't seem so great. If you do want to create a self-signed certificate, you can find Raspberry Pi compatible instructions online [8].

`rewrite` module (you will use this later) with the `a2enmod` `rewrite` command. For the name of this server, I'm using `lodge.local` because that's a proper fully qualified domain name (FQDN), which will not require a DNS lookup to resolve. Set the name of the server in the hostname file:

```
echo `lodge.local` > `/etc/hostname`
```

and add the IP address of that name by appending a line to `/etc/hosts:`

```
10.42.0.1    `lodge.local`
```

(You will remove this entry later.) At the end of `/etc/apache2/apache2.conf` add:

```
ServerName `lodge.local`
```

Now things are getting interesting. Remember this server isn't going to be on the Internet. Later, when you set up the DNS, you're going to redirect every domain (hostname) to here. However, that alone isn't quite right. You need to check what host the browser is asking for. If it's not your host, then you need to redirect the browser to your host. In `/etc/apache2/sites-enabled/000-default.conf`, add the code from Listing 3 at the end of the file. Then restart Apache via:

```
systemctl restart apache2
```

# Listing 3: Apache rewrite Rule

```
01  ServerName `lodge.local`
02
03  <If "`%{HTTP_HOST} != 'lodge.local'`">
04      RewriteEngine on
05      RewriteRule `.*` http://lodge.local/ `[redirect=temporary, nocase, last]`
06  </If>
```

# Listing 4: Website (index.html)

```
01  <!DOCTYPE html>
02  `Login as user <b>user</b> with password <b>user</b>`
03  `<a href="`/owncloud`/">`OwnCloud`</a>`
```

# Listing 5: Hotspot Configuration

```
01  `nmcli con add type wifi ifname wlan0 con-name` `lodge` `autoconnect` `yes` `ssid` `lodge`
02  `nmcli con modify` `lodge` `802-11-wireless.mode` `ap` `802-11-wireless.band` `bg` `ipv4.method` `shared`
03  `nmcli con up` `lodge`
04  `nmcli con modify` `lodge` `connection.autoconnect` `yes`
```

This makes captive portal [6] detection work. Recent smartphone and computer operating systems will check a known non-secure URL when first connecting to an access point to see if they're online. (For example, some versions of Windows check `http://www.microsoft.com/connect/connecttest.txt` which returns `Microsoft` `Connect` `Test`.)

I first thought that returning anything but the expected text would make the client OS detect a captive portal, but that didn't work. From experimenting, it appears that the client OS requires an `HTTP` redirect to reliably detect a captive portal, so that's what this Apache directive does. It needs to be a temporary redirect so that it's done every time.

You might ask: Why do you want the access point to be detected as a captive portal? If it isn't, the client OS will say "no connection," thereby misleading the user. Yes, it's true that this access point has no connection to the Internet, but it does have its own website. When a captive portal is detected, the user will be instructed to log in, upon which the user will see the website, or more precisely, whatever content you put in `/var/www/html/index.html`, replacing Apache's default page. Listing 4 shows a minimal HTML file that links to the `ownCloud` login page; Figure 5 shows the slightly more polished version I've created for the lodge (1) and how users can navigate