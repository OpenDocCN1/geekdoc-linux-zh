# Networking and Internet Services
PART II

ServerAdmin

The ServerAdmin directive should be set to the address of the Webmaster managing the server. It should be a valid email address or alias, such as webmaster@your_domain.com. Setting this value to a valid address is important because this address will be returned to a visitor when a problem occurs on the server.

ServerName

The ServerName directive sets the hostname the server will return. Set it to a fully qualified domain name (fqdn). For example, set it to www.your_domain.com rather than simply www. This is particularly important if this machine will be accessible from the Internet rather than just your local network. You really do not need to set this unless you want a different name returned than the machine's canonical name. If this value is not set, the server will figure out the name by itself and set it to its canonical name. However, you might want the server to return a friendlier address, such as intranet.website.for.your. Whatever you do, ServerName should be a real Domain Name System (DNS) name for your network. If you are administering your own DNS server, remember to add an alias for your host. If someone else manages the DNS for you, ask that person to set this for you.

DocumentRoot

If you are using virtual hosts and are administering your own domains, consider adding a second host entry for your domain without the www prefix. This would mean that someone typing http://yourdomain.com would also get to your web site just the same as typing http://www.yourdomain.com.

Set this directive to the absolute path of your document tree, which is the top directory from which Apache will serve files. By default, SuSE set it to /usr/local/httpd/htdocs; if you built the source code yourself, the default location is /usr/local/apache/htdocs. Prior to version 1.3.4, this directive appears in smrm.conf.

UserDir

This directive defines the directory relative to a local user's home directory where that user can publish HTML documents. It's relative because setting for this directive each user will have his own HTML directory. The default setting for this directive is public_html. Each user will be able to create a directory public_html under his home directory, and HTML documents placed in that directory will be available as http://servername/-username, where username is the username of the