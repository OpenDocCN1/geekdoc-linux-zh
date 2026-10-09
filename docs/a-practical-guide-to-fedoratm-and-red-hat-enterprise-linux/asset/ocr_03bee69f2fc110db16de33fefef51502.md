negotiation (mod_negotiation.so) Allows content negotiation.
proxy (mod_proxy.so) Allows Apache to act as a proxy server.
proxy_connect (mod_proxy_connect.so) Allows connect request handling.
proxy_ftp (mod_proxy_ftp.so) Provides an FTP extension proxy.
proxy_http (mod_proxy_http.so) Provides an HTTP extension proxy.
rewrite (mod_rewrite.so) Allows on-the-fly URI rewriting based on rules.
setenvif (mod_setenvif.so) Sets environment variables based on a request.
speling (mod_speling.so) Auto-corrects spelling if the requested URL has incorrect capitalization and one spelling mistake.
status (mod_status.so) Allows the server status to be queried and viewed.
unique_id (mod_unique_id.so) Generates a unique ID for each request.
userdir (mod_userdir.so) Allows users to have content directories (public_html).
usertrack (mod_usertrack.so) Allows tracking of user activity on a site.
virtual_host_alias (mod_vhost_alias.so) Allows the configuration of virtual hosting.

# mod_cgi AND CGI SCRIPTS

The CGI (Common Gateway Interface) allows external application programs to interface with Web servers. Any program can be a CGI program if it runs in real time (at the time of the request) and relays its output to the requesting client. Various kinds of scripts, including shell, Perl, Python, and PHP, are the most commonly encountered CGI programs because a script can call a program and reformat its output in HTML for a client.

Apache can handle requests for CGI programs in several different ways. The most common method is to put a CGI program in the cgi-bin directory and then enable its execution from that directory only. The location of the cgi-bin directory, as specified by the ScriptAlias directive (page 958), is /var/www/cgi-bin. Alternatively, an AddHandler directive (page 952) can identify the filename extensions of scripts, such as .cgi or .pl, within the regular content (e.g., AddHandler cgi-script .cgi). If you use AddHandler, you must also specify the ExecCGI option in an Options directive within the appropriate <Directory> container. The mod_cgi module must be loaded to access and execute CGI scripts.

The following Perl CGI script displays the Apache environment. This script should be used for debugging only because it presents a security risk if remote clients can access it:

```
```
#!/usr/bin/perl

## prIntenv -- demo CGI program that prints its environment
##


print "Content-type: text/plain\n\n";
foreach $var (sort(keys(%ENV))) {
	$val = $ENV{$var};
	$val =~ s/\n/\\n/g;
	$val =~ s/\t/\\t/g;
	print "$var=$"$val)"\n";
}
```
```