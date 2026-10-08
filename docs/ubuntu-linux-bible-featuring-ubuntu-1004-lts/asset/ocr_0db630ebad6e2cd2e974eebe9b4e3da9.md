# # Configuring Apache

As mentioned in the previous section, the configuration files for the Apache 2 Web server are located in the directory /etc/apache2. Configuration files for web-sites that are available in an Apache 2 Web server are located in the directory /etc/apache2/sites-available. To actually support a site from your Web server, you must create a configuration file for that Web server in /etc/apache2/site-available, and then create symbolic links to point that configuration file in the /etc/apache2/sites-available directory.

The only web site that is out-of-the-box with a standard Apache 2 installation is its default web site, which displays the web page shown in Figure 29-1.

**Figure 29-1**

The default page for a newly installed Apache 2 Web server

![](bbox=[0.043, 0.396, 0.693, 0.655])

# # Note

If you are creating a new web site and want it to be your Web server's default page, you can simply put your content in the /var/www directory, where things would work fine immediately.

The following is a listing of the file /etc/apache2/sites-available/default, which activates the site on this server. (I' added line numbers to make it easier to refer to different entries—they do not actually appear in the file!)

+   1. <VirtualHost *:80>
2. ServerAdmin webmaster@localhost