The following illustrates this process:

# Figure 6-5

![](bbox=[0.32, 0.15, 0.89, 0.48])

# Configure a Virtual Host

For every virtual host you need to create a configuration file in the directory /etc/apache2/vhosts.d/. The name of the configuration file has to end with .conf.

You can find a template file vhost.template in the directory /etc/apache2/vhosts.d/ to use as a base for your configuration file.

You need to edit the following directives in the template:

# Table 6-2

| Directive | Description |
| --- | --- |
| ServerAdmin | Enter the email address of the Virtual Host administrator here. |