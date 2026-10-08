# PART 2 | Layered Security and Linux

If you use MySQL, be sure to open port 3306 on any firewall between the Web server and MySQL database server. Don't open that port on an external firewall (unless required for other reasons). If you prefer a different port, it's easy to configure in the main MySQL configuration file with the port directive.

The first time you install MySQL on Debian-style systems, including Ubuntu, the installation process prompts you for a MySQL root password. This user is different from the standard Linux root administrative user, and should be configured with a different password. To set that password differently, use the mysqladmin command, similar to the following. In this command, the quotes are required around the new password.

corporate sponsor of MySQL, the future of this open source database system is unknown. Oracle has its own excellent database systems. Fortunately, excellent open source database alternatives are available, In fact, Red Enterprise Linux includes PostgreSQL and MySQL packages in its repositories. For more information, see http://www.postgresql.org.

```
# mysqladmin -u root password "newpassword"
```

Unless a MySQL root account is configured, any hacker on the local system has access to the MySQL database. That could be a significant security issue.

# Apache Scripting Languages

The installation of any scripting language should be a red flag for any security professionals. If a black-hacker breaks into a system, that person could use that language to build more powerful malware within your network. However, a scripting language of some sort is normally required for an enterprise-level Web site. When installing a group of packages such as the LAMP stack, it helps to choose one scripting language.

It's easier to monitor news for one scripting language for security updates. If multiple languages are installed, uninstall all but one if possible.

# Apache Modules

One of the strengths of the Apache web server is its modularity. If you have access to both Red Hat and Ubuntu systems, examine the differences. You'll learn more about how Apache can be configured. One list of modules is shown in Figure 9-1.

The process for disabling a module depends on how the Apache configuration files are set up. Current Ubuntu systems include mods-available/ and mods-enabled/ subdirectories in /etc/apache2/ directory. As the names suggest, those subdirectories list and enabled modules. Obviously, it's the package associated with the module that is uninstalled. But you can also use the a2dismod command. For example, the following command removes the PHP version 5 (php.conf, php.load) configuration files from the mods-enabled/ directory:

```
# a2dismod php5
```