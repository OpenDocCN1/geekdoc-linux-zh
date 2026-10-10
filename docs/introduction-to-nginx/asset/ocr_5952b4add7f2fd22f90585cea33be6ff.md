```
gacanepa@ubuntu0S:~/nginx-1.5.6$ sudo checkinstall -D make install
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
gacanepa@ubuntu0S:~/nginx-1.5.6$ aptitude search nginx
i   nginx                                   - Nginx v1.5.6
p   nginx-common                            - small, but very powerful and efficient web server (co
p   nginx-doc                               - small, but very powerful and efficient web server (co
```

Figure 1.22: screenshot

# 1.6  Installing Nginx in CentOS 6.4

# 1.6.1  From repositories

+   *   Download and install nginx yum configuration file from `http://nginx.org/packages/centos/6`. Make sure you select the appropriate architecture; `"noarch"` is a safe choice:
+       *   Download: `wget http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm`