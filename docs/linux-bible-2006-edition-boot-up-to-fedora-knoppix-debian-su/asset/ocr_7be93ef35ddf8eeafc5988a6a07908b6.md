# Operating Your LAMP Server

With the components of your LAMP server installed and running, you are ready to configure Apache and try it out. For this example, Apache is set up to serve content for your domain using a feature virtual hosting, after which you'll see how to install the Coppermine Photo Gallery program, which enables you to create an online photo gallery on your LAMP server.

# Editing Your Apache Configuration Files

The configuration files for Apache HTTPD are incredibly flexible, meaning that you can configure the server to behave in almost any manner you want. This flexibility comes at the cost of increased complexity in the form of a large number of configuration options (directives), but in practice there are only a few directives which you will need to master.

> Note See http://http.apache.org/docs/ for a complete list of directives supported by Apache.

In Debian, Apache configuration is stored in text files read by the Apache server, beginning with /etc/apache/httpd.conf. Configuration is read from start to finish, with most directives being processed in the order in which they are read.

Additional files may also be read by the AccessConfig, ResourceConfig, and Include directives. On modern installations, the AccessConfig and ResourceConfig options point to entry files, and the traditional contents of those files have been moved to the main httpd.conf file.

The Include directive is distinct from AccessConfig and ResourceConfig in it can appear more than once and can include more than one file at a time. Files referenced by Include directives are processed as if their contents appeared at the location of the relevant Include statement. Include can point to a single file, to a directory in which all files are read, or to a wildcard that specifies a specific set of files within a directory.

> Note Subdirectories are also processed when Include points to a directory.

The scope of any configuration directives can be altered based on context. In other words, some parameters may be set on a global level and then changed for a specific file, directory, or virtual host. Other directives are always global in nature, such as those specifying IP addresses the server listens on, and are valid only when applied to a specific location.