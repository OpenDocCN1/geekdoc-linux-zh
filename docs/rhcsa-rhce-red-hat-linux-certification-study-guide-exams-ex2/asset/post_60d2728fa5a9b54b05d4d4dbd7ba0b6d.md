
## TWO-MINUTE DRILL

Here are some of the key points from the certification objectives in Chapter 14.

### The Apache Web Server
- Red Hat Enterprise Linux includes the Apache web server, which is currently used by more than twice as many Internet web sites as all other web servers combined.
- You can install Apache and associated packages as part of the “Web Server” package group.
- Apache configuration files include httpd.conf in the /etc/httpd/conf directory and ssl.conf in the /etc/httpd/conf.d directory.
- Log information for Apache is available in the /var/log/httpd directory.

### Standard Apache Security Configuration
- Apache can be secured through iptables rules and various SELinux booleans and contexts.
- Apache supports security by specifying active ports through the Listen and NameVirtualHost directives.
- Apache supports host-based security by IP address or domain name.
- Apache supports user-based security by password, with the help of the htpasswd command.

### Specialized Apache Directories
- Apache makes it easy to set up access to user home directories, in their public_html/ subdirectories.
- Group-managed directories can be configured in a fashion similar to user home directories.

### Regular and Secure Virtual Hosts
- [ ] You can configure multiple web sites on your server, even with only one IP address. This is possible through the use of virtual hosts.
- [ ] The RHEL configuration supports the configuration of virtual hosts for regular web sites at the end of the `/etc/httpd/conf/httpd.conf` file.
- [ ] The RHEL configuration supports the configuration of secure virtual hosts for regular web sites at the end of the `/etc/httpd/conf.d/ssl.conf` file.
- [ ] SSL certificates can be created with the `genkey` command, when run from the `/etc/pki/tls/certs` directory.

### Deploy a Basic CGI Application
- [ ] The use of CGI content depends on configuration options like ScriptAlias, ExecCGI, and AddHandler cgi-script.
- [ ] Standard CGI scripts require 755 permissions. If needed, sample instructions are available in the Apache manual available from the httpd-manual package.

![](img/9139201cfcaf4292284a0eed074928e5_813_0.png)

![](img/9139201cfcaf4292284a0eed074928e5_814_0.png)

## SELF TEST

The following questions will help measure your understanding of the material presented in this chapter. As no multiple-choice questions appear on the Red Hat exams, no multiple-choice questions appear in this book. These questions exclusively test your understanding of the chapter. It is okay if you have another way of performing a task. Getting results, not memorizing trivia, is what counts on the Red Hat exams. There may be more than one answer to many of these questions.

### The Apache Web Server
1. What is the Apache directive that specifies the base directory for configuration and log files?

2. Once you've modified httpd.conf, what command would make Apache reread this file, without kicking off currently connected users?

3. What directive specifies the TCP/IP port associated with Apache?

### Standard Apache Security Configuration
4. What command creates the /etc/httpd/passwords file and configures a password for user elizabeth?

5. If you see the following directives limiting access within the stanza for a virtual host, what computers are allowed access?

6. What standard ports do you need to open in a firewall to allow access to a regular web site and a secure one?

```
Order Allow,Deny
Allow from 192.168.0.0/24
```

### Specialized Apache Directories
7. What regular permissions would work with a home directory that's shared via Apache?

8. What regular permissions would work with a shared group directory that's also shared via Apache?

### Regular and Secure Virtual Hosts
9. What file does RHEL provide to help configure a virtual host as a secure server?

10. If you're creating a name-based virtual host, how many IP addresses would be required for three virtual servers?

11. To verify the configuration of one or more virtual hosts, what switch can you use with the httpd command?

### Deploy a Basic CGI Application
12. What option with the Options directive supports dynamic CGI content in an Apache configuration file?

## LAB QUESTIONS

Several of these labs involve configuration exercises. You should do these exercises on test machines only. It's assumed that you're running these exercises on virtual machines such as KVM. For this chapter, it's also assumed that you may be changing the configuration of a physical host system for such virtual machines.

Red Hat presents its exams electronically. For that reason, the labs in this and future chapters are available from the CD that accompanies the book, in the Chapter14/ subdirectory. In case you haven't yet set up RHEL 6 on a system, refer to Chapter 1 for installation instructions.

The answers for each lab follow the Self Test answers for the fill-in-the-blank questions.

![](img/9139201cfcaf4292284a0eed074928e5_816_0.png)

## SELF TEST ANSWERS

### The Apache Web Server
1. The ServerRoot directive sets the default directory for the Apache server. Any files and directories not otherwise configured—or configured as a relative directory—are set relative to ServerRoot.
2. There are two basic ways to make Apache reread the configuration file without restarting the service. You can keep Apache running and make it reread the file with a command such as `apachectl graceful` or the `/etc/init.d/httpd reload` command. The `service httpd reload` command is also the acceptable answer.
3. The Listen directive specifies the TCP port associated with Apache.

### Standard Apache Security Configuration
4. The command that creates the `/etc/httpd/passwords` file and configures a password for user elizabeth is `htpasswd -c /etc/httpd/passwords elizabeth`. If `/etc/httpd/passwords` already exists, all that's required is `htpasswd elizabeth`.
5. As described in the chapter, the Order Allow,Deny directive denies access to all systems by default, except those explicitly allowed access. So access is limited to computers on the 192.168.0.0/24 network.
6. The standard ports you need to open in a firewall to allow access to regular and secure web sites are 80 and 443.

### Specialized Apache Directories
7. The associated permissions are 701, executable permissions for other users. As "regular permissions" are specified, ACLs are not an option.
8. The associated permissions are 2771, which combines SGID permissions, standard permissions for a shared group directory, and executable permissions for other users. As "regular permissions" are specified, ACLs are not an option.

### Regular and Secure Virtual Hosts
9. The file associated with secure servers for virtual hosts is ssl.conf in the /etc/httpd/conf.d directory.
10. One IP address is required for a name-based virtual server, no matter how many virtual sites are configured.
11. To check your configuration of virtual hosts, you can use one of two switches with the httpd command: httpd -S checks the configuration file, including virtual host settings. Alternatively, httpd -D DUMP_VHOSTS focuses on the virtual host configuration, and is therefore also an acceptable answer.

### Deploy a Basic CGI Application
12. The Options ExecCGI directive is commonly used in Apache-configured directories that contain CGI scripts such as Perl programs.

## LAB ANSWERS

### Lab I
First, make sure the Apache web server is installed. If an rpm -q httpd command tells you that it is missing, the Web Server package group has not yet been installed. The most efficient way to do so is with the yum groupinstall "Web Server" command. (To find appropriate package group names, run the yum grouplist command.) This assumes a proper connection to a repository, as discussed in Chapter 7.

To configure Apache to start, run the apachectl start command. To make sure it starts the next time the system is booted, run the chkconfig httpd on command.

Once Apache is installed, you should be able to access it from a browser via http://localhost. From the default Apache configuration file, you can verify that the DocumentRoot is located in /var/www/html. You can copy the index.html file from the /usr/share/doc/HTML/en-US directory to the /var/www/html directory. Then you can test the result by navigating once again to http://localhost. If you did not copy the other files associated with the default home page, the display will be missing some icons, but that's not an issue for this lab.
