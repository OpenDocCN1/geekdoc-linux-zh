
## 4. Client-Side Configuration: Configuring Web Browsers to Use Your Squid Server

Flushing firewall rules: [ OK ]
Setting chains to policy ACCEPT: filter [ OK ]
Unloading iptables modules: [ OK ]
Applying iptables firewall rules: [ OK ]
Loading additional iptables modules: ip_conntrack_netbios_n[ OK ]

Let's now learn to configure client-side configuration using the Squid configuration.

You need to configure your PC browser’s proxy server settings manually to use the Squid server. The method you use depends on your browser.

For example, to make these changes using Internet Explorer:

1. Click on the Tools item in the browser’s menu bar.
2. Click on Internet Options.
3. Click on Connections.
4. Click on LAN Settings.
5. Configure with the address and TCP port (3128 default) used by your Squid server. Figure 1 is showing Proxy Server settings in Internet Explorer.

![](img/f3b9cff79e19317416c12eaf5ded7245_183_0.png)

Figure 2 is showing address of Proxy Server along with Port number.

![](img/f3b9cff79e19317416c12eaf5ded7245_184_0.png)

▲ Figure 2

Here’s how to make the same changes using Mozilla or Firefox:

1. Click on the Edit item in the browser’s menu bar.
2. Click on Preferences.
3. Click on Advanced.
4. Click on Proxies.
5. Advanced Configuration of SQUID Proxy Server:

In advanced configuration of Squid proxy server you learn the access control lists.

### Access Control Lists

You can limit users’ ability to browse the Internet with access control lists (ACLs). Each ACL line defines a particular type of activity, such as an access time or source network; they are then linked to an http_access statement that tells Squid whether or not to deny or allow traffic that matches the ACL.

Squid matches each Web access request it receives by checking the http_access list from top to bottom. If it finds a match, it enforces the allow or deny statement and stops reading further. You have to be careful not to place a deny statement in the list that blocks a similar allow statement below it. The final http_access statement denies everything, so it is best to place new http_access statements above it.

Let’s now learn to restrict Web access by time.

### Restricting Web Access by Time

You can create access control lists with time parameters. For example, you can allow only business hour access from the home network:

```
#
# Add this to the bottom of the ACL section of squid.conf
#
acl home_network src 172.16.1.0/24
acl business_hours time M T W H F 9:00-17:00

#  
# Add this at the top of the http_access section of squid.conf
#
http_access allow home_network business_hours
```

Or, you can allow morning access only:

```
#
# Add this to the bottom of the ACL section of squid.conf
#
acl mornings time 08:00-12:00

#  
# Add this at the top of the http_access section of squid.conf
#
http_access allow mornings
```

### Restricting Web Access by IP Address

You can create an access control list that restricts Web access to users on certain networks. In this case, it’s an ACL that defines a home network of 172.16.1.0:

```
#  
# Add this to the bottom of the ACL section of squid.conf
#
acl our_network src 172.16.1.0/255.255.255.0
```

You also have to add a corresponding http_access statement that allows traffic that matches the ACL:

```
#  
# Add this at the top of the http_access section of squid.conf
#
http_access allow our_network
```

### Squid proxy authentication using ncsa_auth helper

For fine control you may need to use Squid proxy server authentication. This will only allow authorized users to use proxy server.

You need to use proxy_auth ACLs to configure ncsa_auth module. Browsers send the user’s authentication in the Authorization request header. If Squid gets a request and the http_access rule list gets to a proxy_auth ACL, Squid looks for the Authorization header. If the header is present, Squid decodes it and extracts a username and password.

However squid is not equipped with password authentication. You need to take help of *authentication helpers*. Following are included by default in most squid and most Linux distros:

- NCSA: Uses an NCSA-style username and password file.
- LDAP: Uses the Lightweight Directory Access Protocol
- MSNT: Uses a Windows NT authentication domain.
- PAM: Uses the Linux Pluggable Authentication Modules scheme.
- SMB: Uses a SMB server like Windows NT or Samba.
- getpwnam: Uses the old-fashioned Unix password file.
- SASL: Uses SASL libraries.
- NTLM: Negotiate and Digest authentication

Let's now learn to configure an NCSA.

### Configure an NCSA-style username and password authentication

First create a NCSA password file using `htpasswd` command. `htpasswd` is used to create and update the flat-files used to store usernames and password for basic authentication of squid users.

```
[root@netmon tmp]#htpasswd /etc/squid/passwd user1

Output:
New password:
Re-type new password:
Adding password for user user1
```

Make sure squid can read passwd file:

```
[root@netmon tmp]#chmod o+r /etc/squid/passwd
```

### Locate ncsa_auth authentication helper

Usually `ncsa_auth` is located at `/usr/lib/squid/ncsa_auth`. You can find out location using `rpm` (Rhedat and Fedora)
If you are using RHEL/Fedora Core or RPM based distro try:

```
# rpm -qI squid | grep ncsa_auth

Output:
/usr/lib/squid/ncsa_auth
```

### Configure ncsa_auth for squid proxy authentication

Now open /etc/squid/squid.conf file

```
[root@netmon tmp]#vi /etc/squid/squid.conf
Append (or modify) following configuration directive:
auth_param basic program /usr/lib/squid/ncsa_auth /etc/squid/passwd
auth_param basic children 5
auth_param basic realm Squid proxy-caching web server
auth_param basic credentialsttl 2 hours
auth_param basic casesensitive off

Also find out your ACL section and append/modify
acl ncsa_users proxy_auth REQUIRED
http_access allow ncsa_users
```

Save and close the file.

- auth_param basic program /usr/lib/squid/ncsa_auth /etc/squid/passwd : Specifies squid password file and helper program location
- auth_param basic children 5 : Contains the number of authenticator processes to spawn.
- auth_param basic realm Squid proxy-caching web server : Contains the part of the text the user will see when prompted their username and password
- auth_param basic credentialsttl 2 hours : Specifies how long squid assumes an externally validated username:password pair is valid for - in other words how often the helper program is called for that user with password prompt. It is set to 2 hours.
- auth_param basic casesensitive off : Specifies if usernames are case sensitive. It can be on or off only
- acl ncsa_users proxy_auth REQUIRED : Requires any authenticated user will match the ACL named ncsa_users
- http_access allow ncsa_users : Allows proxy access only if user is successfully authenticated.

Type the following command to restart the Squid server.

```
[root@netmon tmp]#/etc/init.d/squid restart
```

Let’s now learn to monitor the Squid proxy server.

## Monitoring Squid proxy server

### Logging

Log files can be found in /var/log/squid

See access log file /var/log/squid/access.log:

- [root@netmon tmp]#tail -f /var/log/squid/access.log

Above command will monitor all incoming request and log them to /var/log/squid/access.log file. Now if somebody accessing a website through browser, squid will log information.

- Tools: Various tools can be used to analyze these log files. One such tool is Webalizer. Webalizer gives useful statistics in with graphs. The following is a simple Webalizer example:

```
[root@netmon tmp]#/usr/bin/webalizer -F squid /var/log/squid./access.log
```

Webalizer will process the logfile and place the results in /var/lib/webalizer/. To view the results type:

```
[root@netmon tmp]#mozilla /var/lib/webalizer/index.html
```
