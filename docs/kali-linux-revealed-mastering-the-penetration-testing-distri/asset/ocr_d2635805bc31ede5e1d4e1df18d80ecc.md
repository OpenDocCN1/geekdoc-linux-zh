offsec-defaults_1.0_all.deb, and offsec-defaults_1.0_amd64.changes) into /tmp/ on the server hosting the package repository and ask reprepro to include the package:

```
$ reprepro include offsec-internal /tmp/offsec-defaults_1.0_amd64.changes
Exporting indices...
$ find pool
pool
pool/main
pool/main/o
pool/main/o/offsec-defaults
pool/main/o/offsec-defaults/offsec-defaults_1.0.dsc
pool/main/o/offsec-defaults/offsec-defaults_1.0.tar.xz
pool/main/o/offsec-defaults/offsec-defaults_1.0_all.deb
```

As you can see, it added the files into its own package pool in a pool sub-directory.

The dists and pool directories are the two directories that you need to make (publicly) available over HTTP to finish the setup of your APT repository. They contain all the files that APT will want to download.

Assuming that you want to host this on a virtual host named pkgrepo.offsec.com, you could create the following Apache configuration file, save it to /etc/apache2/sites-available/pkgrepo.offsec.com.conf, and enable it with a2ensite pkgrepo.offsec.com):

```
<VirtualHost *:80>
ServerName pkgrepo.offsec.com
ServerAdmin repoadmin@offsec.com

ErrorLog /var/log/apache2/pkgrepo.offsec.com-error.log
CustomLog /var/log/apache2/pkgrepo.offsec.com-access.log "%h %l %u %t "%r" %>s "%0"

DocumentRoot /home/pkgrepo/reprepro

<Directory "/home/pkgrepo/reprepro">
Options Indexes FollowSymLinks MultiViews
Require all granted
AllowOverride All
</Directory>
</VirtualHost>
```

And the corresponding sources.list entry to add on machines that need packages from this repository would look like this:

```
deb http://pkgrepo.offsec.com offsec-internal main

# Enable next line if you want access to source packages too
# deb-src http://pkgrepo.offsec.com offsec-internal main
```

Your package is now published and should be available to your networked hosts.