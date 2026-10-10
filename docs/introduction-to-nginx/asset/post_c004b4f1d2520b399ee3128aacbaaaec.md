
start-stop-daemon --start --quiet --pidfile /var/run/$NAME.pid \
--exec $DAEMON -- $DAEMON_OPTS || true
echo "$NAME."
;;

![](img/3adf2b91cc40e3d0012eab041f055ca8_14_0.png)

![](img/3adf2b91cc40e3d0012eab041f055ca8_14_1.png)

![](img/3adf2b91cc40e3d0012eab041f055ca8_14_2.png)

## 1.5 Use of the checkinstall package to keep track of all the files created or modified by an installation script

The checkinstall package (see Fig. 1.19) keeps track of all the files created or modified during the installation process. It also creates and installs a package (.deb or .rpm) that is compatible with your package manager (see Figs. 16 and 17), which can be used later to completely remove the package if you don't need it anymore. Check the attached man page for details on its use.

```
gacanepa@ubuntuOS:~/nginx-1.5.6$ sudo aptitude install checkinstall
[sudo] password for gacanepa:
The following NEW packages will be installed:
build-essential[?] checkinstall dpkg-dev[?] fakeroot[?] g++[?] g++-4.6[?] libalgorithm-diff-perl[?] libalgorithm-diff-xs-perl[?] libalgorithm-merge-perl[?] libdpkg-perl[?] libstdc++6-4.6-dev[?]
0 packages upgraded, 11 newly installed, 0 to remove and 72 not upgraded.
Need to get 9,326 kB of archives. After unpacking 27.7 MB will be used.
Do you want to continue? [Y/n/?] Y
```

![](img/3adf2b91cc40e3d0012eab041f055ca8_14_3.png)

```
gacanepa@ubuntuOS:~/nginx-1.5.6$ sudo checkinstall -D make install
checkinstall 1.6.2, Copyright 2009 Felipe Eduardo Sanchez Diaz Duran
this software is released under the GNU GPL.

The package documentation directory ./doc-pak does not exist.
Should I create a default set of package docs? [y]: y
Preparing package documentation...OK
```

Figure 1.20: Creating a .deb file with checkinstall and make install (I)

```
Done. The new package has been installed and saved to
/home/gacanepa/nginx-1.5.6/nginx_1.5.6-1_i386.deb
You can remove it from your system anytime using:
dpkg -r nginx
```

Figure 1.21: Creating a .deb file with checkinstall and make install (II)

When we run `aptitude search nginx`, the package that we just installed will appear with the comments that we added as description (see Fig. 1.22):

```
gacanepa@ubuntuOS:~/nginx-1.5.6$ aptitude search nginx
i   nginx                                   - Nginx v1.5.6
p   nginx-common                            - small, but very powerful and efficient web server (co
p   nginx-doc                               - small, but very powerful and efficient web server (co
```

Figure 1.22: screenshot

## 1.6 Installing Nginx in CentOS 6.4

### 1.6.1 From repositories

- Download and install nginx yum configuration file from `http://nginx.org/packages/centos/6`. Make sure you select the appropriate architecture; `"noarch"` is a safe choice:
  - Download: `wget http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm`
  - Install: `rpm -ivh nginx-release-centos-6-0.el6.ngx.noarch.rpm`
  - Install nginx: `yum install nginx`
  - Start nginx: `service nginx start`

### 1.6.2 From sources

Follow the same procedure as for Debian and Ubuntu.

### 1.6.3 Enabling modules

According to its wiki (NGINX Wiki Page), Nginx modules must be selected during compile as run-time selection of modules is not currently supported. A full summary of the compile-time options, including optional modules, can be found in the provided configure script by running `./configure --help`. Unfortunately, if we have installed Nginx installed and want to add a certain module, we will have to uninstall it and then recompile it with support for the desired module.

For a list of the standard HTTP modules, refer to Table 1 (NGINX Modules):

Table 1.1: Standard HTTP modules

| Name | Description | Version | configure argument to enable |
| :--- | :--- | :--- | :--- |
| Map | Set config variables using arbitrary key/value pairs. | 0.3.16 | --without-http_map_module |
| Memcached | Memcached support. | | --without-http_memcached_module |
| Proxy | Proxy to upstream servers. | | --without-http_proxy_module |
| Referer | Filter requests based on Referer header. | | --without-http_referer_module |
| Rewrite | Request rewriting using regular expressions. | | --without-http_rewrite_module |
| SCGI | SCGI protocol support. | 0.8.42 | --without-http_scgi_module |
| Split Clients | Splits clients based on some conditions | 0.8.37 | --without-http_split_clients_module |
| SSI | Server-side includes. | | --without-http_ssi_module |
| Upstream | For load-balancing. | | --without-http_upstream_ip_hash_module<br>(ip_hash directive only) |
| User ID | Issue identifying cookies. | | --without-http_userid_module |
| uWSGI | uWSGI protocol support. | 0.8.40 | --without-http_uwsgi_module |
| X-Accel | X-Sendfile-like module. | | |

For a list of option HTTP modules, refer to Table 2:

Table 1.2: Optional HTTP modules

| Name | Description | Version | configure argument to enable |
| :--- | :--- | :--- | :--- |
| Addition | Append text to pages. | | --with-http_addition_module |
| Auth Request | Implements client authorization based on the result of a subrequest. | 1.5.4 | --with-http_auth_request_module |
| Degradation | Allow to return 204 or 444 code for some locations on low memory condition. | 0.8.25 | --with-http_degradation_module |
| Embedded Perl | Use Perl in Nginx config files. | 0.3.21 | --with-http_perl_module |
| FLV | Flash Streaming Video | 0.4.7 | --with-http_flv_module |
| GeoIP | Creates variables with information from the MaxMind GeoIP binary files. | 0.8.6, 0.7.63 | --with-http_geoip_module |
| Google PerfTools | Google Performance Tools support. | 0.6.29 | --with-google_perftools_module |
| Gzip Precompression | Serves precompressed versions of static files. | 0.6.23 | --with-http_gzip_static_module |
| Gunzip | On-the-fly decompressing of gzipped responses. | 1.3.6 | --with-http_gunzip_module |
| Image Filter | Transform images with Libgd | 0.7.54 | --with-http_image_filter_module |
| MP4 | Enables mp4 streaming with seeking ability. | 1.1.3, 1.0.7 | --with-http_mp4_module |
| Random Index | Randomize directory indexes. | 0.7.15 | --with-http_random_index_module |
| Real IP | For using nginx as backend | 0.3.8 | --with-http_realip_module |
| Secure Link | Protect pages with a secret key | 0.7.18 | --with-http_secure_link_module |
| SSL | HTTPS/SSL support. | | --with-http_ssl_module |
| Stub Status | View server statistics. | 0.1.18 | --with-http_stub_status_module |
| Substitution | Replace text in pages | | --with-http_sub_module |
| WebDAV | WebDAV pass-through support. | 0.3.38 | --with-http_dav_module |
| XSLT | Post-process pages with XSLT. | 0.7.8 | --with-http_xslt_module |

For a list of mail modules, refer to Table 3:

Table 1.3: Mail modules

| Name | Description | configure argument |
| :--- | :--- | :--- |
| Mail Core | Core parameters for mail module. | --with-mail |
| POP3 | POP3 settings. | --without-mail_pop3_module |
| IMAP | IMAP settings. | --without-mail_imap_module |
| SMTP | SMTP settings. | --without-mail_smtp_module |
| Auth HTTP | Use Nginx to authenticate mail services. | |
| Proxy | Nginx can proxy IMAP, POP3, and SMTP protocols. | |
| SSL | This module ensures SSL/TLS support for POP3/IMAP/SMTP. | --with-mail_ssl_module |

As an example, we will recompile Nginx to include the Addition module (see Fig. 1.23):

![](img/3adf2b91cc40e3d0012eab041f055ca8_18_0.png)

Figure 1.23: Recompiling Nginx with the Addition module

## 1.7 Adding Nginx as a system service

- Debian / Ubuntu: `update-rc.d -f nginx defaults` (use sudo on Ubuntu)

Note: If any files /etc/rcrunlevel.d/[SK]?name already exist then update-rc.d does nothing. The program was written this way so that it will never change an existing configuration, which may have been customized by the system administrator. The program will only install links if none are present, i.e., if it appears that the service has never been installed before.

- CentOS: `chkconfig nginx on`

# Chapter 2

# Nginx Configuration Guide

### 2.1 Configuration file syntax

According to Merriam-Websters online dictionary, the word syntax represents "the way in which words are put together to form phrases, clauses, or sentences". Of course that definition, as it is taken from a dictionary, is aimed at English (or actually any other language) students. So what about IT people coming from all backgrounds, languages, and countries? The change in context does not alter the meaning of the term very significantly. In particular, the syntax of a configuration file must be correct, as seen by the program that will parse it, in order for it to work efficiently.

We will learn to understand and how to write (and / or modify) a configuration file for Nginx under Ubuntu 12.04 LTS. That will be accomplished by specifying a set of values that will define the behavior of the web server.

### 2.2 Configuration directives

By default, the behavior of Nginx is defined by its main configuration file, which is located (as seen before and unless we have modified this setting) at `/usr/local/nginx/conf/nginx.conf`. This file is composed of a list of directives organized in a logical structure that is very easy to follow and understand (see Fig. 2.1).
