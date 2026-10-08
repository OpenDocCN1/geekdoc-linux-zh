
# PART 2 | Layered Security and Linux

## Do Not Allow Overrides with .htaccess

An .htaccess file can be a handy way to add Apache directives for specific directories or virtual hosts. With the dot in front, it's a hidden file, and the .htaccess file can be dangerous. It's outside the view of a normal search.

If a black-hat hacker is able to add an .htaccess to a Web server directory, that user can override anything you've configured with directives in that file. To disable the use of .htaccess, add the following directive in stanza with the Directory tag:

```AllowOverride None
```

## Do Not Allow Access to User Directories

It's probably too easy to configure access to user home directories on the system with the Apache server. With the mod_userdir module and the UserDir enable directive, user directories can be shared over the Apache web server. Unless you want files in user home directories exposed to the world, it's something to disable.

To disable Apache-based access to user home directories, disable the mod_userdir module. If you're not prepared to do that, at least avoid the UserDir enable directive unless the system includes only guest accounts with files that can be shared publicly.

## Minimize Options

The Options directive is important. It allows you to configure extra features within a Directory stanza. The default setting is Options All, which includes a number of features shown in Table 9-3 that are inconsistent with a secure system. It includes all features except MultiViews.

Each of these Options directives may be a potential security risk. Because the default includes all one of the directives, any black-hat hacker is able to insert a file into one of the listed directories may cause problems. Alternatively, if that user is able to delete an index.html file, it may expose that directory to all who browse that system.

| TABLE 9-3 Apache-Options and associated features |
|---|---|
| ExecCGI | Allows the execution of CGI scripts if the mod_cgi module is enabled |
| FollowSymLinks | Supports the following of symbolically linked files in the |
| Includes | Allows the use of server-side includes if the mod_include module |
| IncludesNOEXEC | Allows the use of server-side includes except for executable files |
| Indexes | Lists files in directories where no DirectoryIndex file, typically index.html, is included if the mod_autoindex module is enabled |
| MultiViews | Supports error-tolerant reads of filenames |
| SymLinksOwnerMatch | Supports the following of symbolically linked files in the directory if the link and the file are owned by the same user |

The way to avoid the security risks associated with Table 9-3 is to disable all Options with the following directive:

```Options None
```

## Configure Protection on a Web Site

Typically, multiple Web sites are configured on individual Apache Web servers. That's made possible with an appropriate configuration of virtual hosts. Web site accessibility can be limited to a certain IP address network with the following directives, which deny access from all systems except that send requests from addresses with the noted IP network address and network mask:

```
Order deny,allow
Deny from all
Allow from 192.168.0.0/255.255.255.0
```

The same group of directives can be used in a stanza for a specific directory. If desired, you can substitute a partial or complete domain name such as example.org.com or the noted IP address.

One other protection system is based on users created with the htpasswd or htdigest commands. If the file with users and passwords is /etc/httpd/conf.d/apacheusers, you could take advantage of the following directives restricting access to a specific Web site or directory:

```
AuthName "Authorized users only"
AuthType Digest
AuthUsersFile /etc/httpd/conf.d/apacheusers
Require valid-user
```

Users who are allowed to access the resource can be limited by username or groupname.

## Configure a Secure Web site

By default, Web sites use the HTTPS protocol use port 443. But enabling the appropriate SSL module requires different commands on different systems. On Red Hat systems, when the mod_ssl package is installed, an ssl.conf file with sample directives for a secure Web site can be found in the /etc/httpd/conf.d/ directory. On Ubuntu systems, when the a2enmod command described earlier is applied to the ssl module, similar directives can also be found in an ssl.conf file, this time in the /etc/apache2/mods-enabled/

Because the contents of these files are normally included in the main Apache configuration file with an Include directive, all you need to do is customize the ssl.conf file for the desired secure Web site. But a secure Web site requires a certificate authority.

![](img/c0608a8c8a0777903dfec4ff61fdffa1_284_0.png)

# PART 2 | Layered Security and Linux

| TABLE 9-4 Certificate authority (CA) file extensions |
| FILE EXTENSION | DESCRIPTION |
| --- | --- |
| .crt | Configured for the server certificate |
| .csr | Created with the certificate signing request |
| .key | Associated with the CA key |

## Configure a Certificate Authority

A certificate authority (CA) is an entity that issues digital certificates. The actual certificates are based on a private/public key pair. While such key pairs can be generated locally, they would not be official CAs associated with major online enterprises. Such key pairs can be expensive. However, "official" CAs are required if you want a Web site that doesn't lead to an "invalid security certificate" error. If you are interested, official CAs are available from companies such as VeriSign and GoDaddy.

The standard filenames associated with CAs are arbitrary. However, there are standard file extensions for CAs, as listed in Table 9-4.

To create a self-signed certificate, you can use the openssl command. For example, the following command creates a CA key named server.key, generated with Rivest, Shamir, Adelman (RSA) parameters, using a 256-bit Advanced Encryption Standard (aes256) cipher of 1024 bytes.

```
# openssl genrsa -aes256 -out server.key 1024
```

This command prompts for a passphrase. Once the server.key file is created, you can create a certificate-signing request file. The following command uses that server.key file to create that server.csr.

```
# openssl req -new -key server.key -out server.csr
```

You're prompted for the following information. If you're setting up an official certificate, the following command creates the server.crt for 30 days.

```
# openssl x509 -req -days 30 -in server.csr -signkey server.key -out server.crt
```

You're prompted for the following information. If you're setting up an official certificate, the following command creates the server.crt for 30 days.

- The country
- The state
- The locality
- The organization
- The organizational unit
- The email-address
- The common name

# CHAPTER 9 | Networked Application Security

# 259
