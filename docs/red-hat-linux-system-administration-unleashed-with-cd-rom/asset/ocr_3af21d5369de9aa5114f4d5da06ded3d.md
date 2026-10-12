all three files. Because Red Hat 6.1 uses all three configuration files in the default Apache rpm, we will cover how to configure Apache using all three files. To edit those configuration files, you can use any text editor, such as vi or pico.

# access.conf

The access.conf file is where all access conditions are defined, the httpd.conf is the main server configuration file, and the srm.conf file is used to set up the server's request handling services. As you begin working with Apache, you should become very familiar with these three files. If you would like to follow the Apache group recommendation and move all directives into the httpd.conf, keeping both access.conf and srm.conf blank, you can do that. However, it may create problems later when you decide to upgrade your Red Hat version.

# Overriding the Configuration Files

You can override the usage of each of the configuration files and tell Apache to use different files. The httpd.conf filename can be overridden by using the -f options on the command line when starting Apache. The srm.conf filename can be overridden by using the ResourceConfig directive. The access.conf filename can be overridden with the AccessConfig directive.

The main idea behind the Apache configuration files is that of configuration directives, each of which instructs the Web server to perform a specific action. Apache has quite a collection of available configuration directives; we will be taking a look at some of them later in this section. You can put comments within the configuration file as well, any line that begins with a pound sign (#) is treated as a comment by Apache. After you make changes to the file, you must restart Apache before any changes will take effect.

When editing the httpd.conf, keep in mind that it is divided into three main sections. The sections are as follows:

+   - **Global Directives**—Directives that are global to the entire Apache server process.
+   - **Main Directives**—Directives that define the main Apache server, all virtual hosts use these settings for their default actions.
+   - **Virtual Host Settings**—The settings for any virtual hosts.

When Apache is first started, it initially processes the contents of the /etc/httpd/httpd.conf file. Following that, the /etc/httpd/srm.conf file is processed, and, finally, the /etc/httpd/access.conf file is processed. As was mentioned earlier, Apache's configuration can be set using only the httpd.conf file, which is the recommended way of doing things, although under Red Hat Linux, all three of the configuration files are used.