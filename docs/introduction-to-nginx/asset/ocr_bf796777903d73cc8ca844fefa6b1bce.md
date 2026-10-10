+   - Install: rpm -ivh nginx-release-centos-6-0,el6.ngx.noarch.rpm

+   - Install nginx: `yum install nginx`

+   - Start nginx: `service nginx start`

# 1.6.2 From sources

Follow the same procedure as for Debian and Ubuntu.

# 1.6.3 Enabling modules

According to its wiki (NGINX Wiki Page), Nginx modules must be selected during compile as run-time selection of modules is not currently supported. A full summary of the compile-time options, including optional modules, can be found in the provided configure script by running `./configure --help`. Unfortunately, if we have installed Nginx installed and want to add a certain module, we will have to uninstall it and the recompile it with support for the desired module.

For a list of the standard HTTP modules, refer to Table 1 (NGINX Modules):

Table 1.1: Standard HTTP modules