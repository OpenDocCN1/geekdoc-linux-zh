# Chapter 11: Configuring the Apache Web Server

# Using Multilevel Configurations

The configuration files described in this chapter apply to every copy of the Apache server started on your system. Apache provides a way, for for different configuration settings depending on the location of the file requested by a user. For example, you might want the overall configuration to block directory listing, but in one area, you want to select from a directory listing because the contents change each day and you don't want to update an HTML page.

Each directory can contain a configuration file that applies to everything in that directory and everything below it. The default name of file is .htaccess (it starts with a period it is a hidden file). You can set its name to anything you choose. You can also set an option so that no local, directory-specific configuration files are be used. This provides additional security and improves performance because the configuration files don't have to be read and implemented for every request processed by the Web server.

The performance hit can be heavy if you use a lot of per-directory configuration files because of the inheritance feature. For example, if a user requests the file /doc/products/reviews/june.html the Web server must check each subdirectory in that path to see whether changes or additions are made to the configuration settings. Anything in the .htaccess file within the directory documents/ must be processed; then changes and additions in the products/ subdirectories are reviewed, then those in reviews/. This must be done for each Web request.

Although it's a useful feature if you really need it, if you don't need per-directory configuration, you'll improve performance and decrease security concerns. The main reason for using per-directory configuration is when different people control sections of your Web site, such as users' home pages, marketing information, and technical support documents.

# Configuration File Layout

Each of the configuration files for the Apache server is a plaintext file that lists options and settings for the server. The syntax is very simple, with the following two types of options:

+   * A Directive (command) followed by the options that apply for that directive

+   * An HTML-style container, such as <Directory directory-name>, where all the directives between the opening and closing tag apply to the directory given in the tag

The directives described in the sections that can appear in any of the three configuration files: httpd.conf, srm.conf, and access.conf. The three files exist mostly for historical reasons. For clarity, however, it's a good idea to keep server-level