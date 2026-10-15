
# You may use the command line option `-S` to verify your virtual host configuration.

```
# configuration.

#

# Use name-based virtual hosting.

#

#NameVirtualHost *

#

# VirtualHost example:

# Almost any Apache directive may go into a VirtualHost container.

# The first VirtualHost section is used for requests without a known

# server name.

#

# <VirtualHost *> 

#    ServerAdmin webmaster@dummy-host.example.com

#    DocumentRoot /www/docs/dummy-host.example.com

#    ServerName dummy-host.example.com

#    ErrorLog  logs/dummy-host.example.com-error_log

#    CustomLog logs/dummy-host.example.com-access_log common

# </VirtualHost>
```

以下是虚拟主机指令的示例，可让您在同一台计算机上托管 `handsonhistory.com` 和 `linuxtoys.net` 两个域名：

```
NameVirtualHost *

<VirtualHost *> 

    DocumentRoot /var/www/handsonhistory

    ServerName www.handsonhistory.com

    ServerAdmin webmaster@handsonhistory.com

    ErrorLog logs/handsonhistory.com-error_log

    CustomLog logs/handsonhistory.com-access_log common

</VirtualHost>

<VirtualHost *> 

    DocumentRoot /var/www/linuxtoys

    ServerName www.linuxtoys.net

    ServerAdmin webmaster@linuxtoys.net

    ErrorLog logs/linuxtoys.net-error_log

    CustomLog logs/linuxtoys.net-access_log common

</VirtualHost>
```
