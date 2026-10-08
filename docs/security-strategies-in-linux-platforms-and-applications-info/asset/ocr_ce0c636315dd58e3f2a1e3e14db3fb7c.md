# CHAPTER 9 | Networked Application Security

# 253

Note that this book does not address the details on how to configure or create a regular or a secure Web site. For an excellent primer on the subject, Rich Bowen and Ken Coar's Apache Cookbook: Solutions and Examples for Apache Administrators, published in 2008 by O'Reilly Media.

# The LAMP Stack

As suggested earlier, the components of the LAMP stack vary depending on the preferred scripting language. This is because a book on Linux, and secure options for Apache are described later in this chapter, the focus of this section is on basic MySQL configuration (SQL is short for structured query language) and the associated scripting languages. This section is just an overview; there many excellent books on both MySQL and each of the noted scripting languages.

> TIP On Ubuntu servers, a quick way to install the packages of the LAMP stack is with the console-based tasksel browser. Run the tasksel command with install all the packages required for the LAMP stack.

The focus of this section is the Apache configuration. The names and directories with these files vary by distribution. For example, on Red Hat systems, the main Apache configuration is httpd.conf in the /etc/httpd/conf/ directory. On Ubuntu systems, the main Apache configuration file is apache2.conf in the /etc/apache2/ directory.

# MySQL and Apache

Many Web sites require access to databases. Those databases may help with authentication, logs, and more. Appropriate packages may include software that links to the desired scripting language, such as Perl, Python, or PHP. Many excellent books on MySQL are available, including Paul Dubois' MySQL (4th Edition), published in 2008 by Addison-Wesley. This just describes security-related directives in the default version of the main MySQL configuration file.

The main MySQL configuration file is .cnf. Depending on the distribution, you may find that in the /etc/ or /etc/mysql/ directory. Security-related directives in the are described in Table 9-1.

| TABLE 9-1 Default security-related MySQL directives in my. .cnf. |
| DIRECTIVE | DESCRIPTION |
| bind-address | IP address of associated network card to which MySQL listens |
| datadir | Directory with MySQL data; may require special protection |
| port | Port number |
| ssl-ca | SSL certificate authority file |
| ssl-cert | SSL certificate file |
| ssl-key | SSL certificate key file |