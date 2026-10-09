```
<VirtualHost 206.171.50.50>
 ServerName www.nitec.com
 ServerAdmin kabi@nitec.com
</VirtualHost>
```

this can be represented as the following:

```
$VirtualHost("206.171.60.60") = {
 ServerName => "www.nitec.com",
 ServerAdmin => 'kabi@nitec.com'
}
```

A slightly more involved example is:

```
$Location("/some_dir_alias/") = {
 AuthUserFile => "/www/nitec/secret/htpasswd",
 AuthType => 'Basic',
 AuthName => 'Subscribers Only Access',
 DirectoryIndex => [qw(welcome.html welcome.htm)],
 Limit => {
 METHODS => 'POST GET',
 require => 'user reader'
 }
};
```

In the preceding, the configuration segment is used to create a restricted area using basic HTTP authentication method for an alias called /some dir alias/. A set of filenames are also defined as directory indexes for this alias.

You can define other containers such as <Directory>, <Files>, and so on in a similar manner. Some example configurations follow.

Assume that you have three Web server systems—host_a, host_b, and host_c—and that host_a is more powerful than host_b, and host_b is more powerful than host_c. To define a <Perl> container that enables you to create a single configuration for all three hosts, follow this example of such an httpd.conf file:

```
<Perl>
 # Get the host name using the Unix hostname utility and store
 # it in the $thisHost variable.
 my $thisHost = '/bin/hostname';
 if ($thisHost =~ /host_a/) {
 # configuration for host_a goes here
 $MinSpareServers = 10;
 $MaxSpareServers = 20;
 $StartServers = 30;
 $MaxClients = 256;
 }
 elsif ($thisHost =~ /host_b/) {
 # configuration for host_b goes here
```