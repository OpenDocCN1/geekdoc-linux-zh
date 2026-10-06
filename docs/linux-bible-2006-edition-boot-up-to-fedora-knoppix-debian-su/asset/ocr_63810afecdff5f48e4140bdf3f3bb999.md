# 650 Part V ♦ Running Servers

+   - php4-domxml—Functions related to processing XML
- php4-gd—The GD library is used for creating images. It is most popular for its graph generation functions.
- php4-ldap—Functions for communicating with LDAP servers.
- php4-mysql—Functions for communicating with a MySQL database server.
- php4-pear—Functions and support programs using the PHP Extension and Application Repository (PEAR). PEAR is similar to the CPAN archive for Perl programs and contains a large number of useful modules. (More information about PEAR modules can be found at http://pear.php.net.)
- php4-postgresql—Functions for communicating with a PostgreSQL database
- php4-snmp—Functions for performing network management using the SNMP protocol.

# Setting Up Your LAMP Server

Before proceeding through the examples in this section, be sure that your Linux operating system is installed and configured. The specific instructions in this section were done on a Debian GNU/Linux. If you try this on a different Linux system, understand that such thing as software packaging, the location of start-up scripts and configuration files, and other features may be different.

When you install your Linux system, you typically choose to install a set of software packages that are appropriate for a workstation or a server. You may choose to set up a server on a system that has been configured with the layout and software packages intended for a workstation. However, that's not recommended unless you are providing services for a very small number of users whom you know well and trust. In fact, many systems administrators don't even like to have the X System and other GUI components installed on a server.

# Installing Apache

The next step toward function a LAMP server is to install the Apache HTTP server, which can be found in the apache package. Use APT to retrieve and install the package:

```
# apt-get install apache
```

During the configuration process, you are asked whether you want to enable the suexec mechanism. The suexec feature ensures the security of CGI applications and is generally recommended. You can change your selection later using debconf to reconfigure the apache package. More information about debconf can be found in Chapter 9.