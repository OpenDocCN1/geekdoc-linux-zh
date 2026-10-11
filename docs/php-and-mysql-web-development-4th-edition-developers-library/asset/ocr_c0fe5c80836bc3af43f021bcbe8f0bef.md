depending on which one is most appropriate for each piece of the job. You may also find it instructive to implement an application in several ways if you have time. This gives you direct experience with different APIs as they apply to your own applications.

If you do not have the software required for using any of the APIs, see Appendix A, “Obtaining and Installing Software”.

Should you be interested in additional MySQL programming information beyond what the following chapters provide, other books are available. The two with which I am most familiar (because I wrote them) are *MySQL and Perl for the Web* (New Riders, 2001) and *MySQL Cookbook*, second edition (O'Reilly, 2006). The first provides extensive coverage of the use of MySQL and DBI in Web environments. The second discusses how to write MySQL programs using Perl DBI, the PHPPEAR DB module, Ruby DBI (similar to Perl DBI), Python’s DB-API interface, and the Java JDBC interface. If you’re interested specifically in Java, see *MySQL and Java Developer’s Guide* (Matthews, Cole, and Gracelick; Wiley, 2003). One of the authors (Mark Matthews) is the creator of MySQL Connector/J, the official Java interface for MySQL.

# 6.2.1 The C API

The C API is used within the context of compiled C programs. It’s a client library that provides an interface for talking to the MySQL server, giving you the capabilities you need for establishing a connection to and conversing with the server.

The C clients provided in the MySQL distribution are based on this API. The C client library also serves as the basis for most of the MySQL bindings for other languages. For example, the MySQL-specific driver for the Perl DBI module is made *MySQL*-aware by linking in the code for the MySQL C client library.

# 6.2.2 The Perl DBI API

The DBI API is used within the context of applications written for the Perl scripting language. This API tries to work with as many databases as possible, while at the same time hiding database-specific details from the script writer. DBI does this using Perl modules that work together in a two-level architecture (see Figure 6.1):

+   - The DBI (database interface) level provides the general-purpose interface for client scripts. This level provides an abstraction that does not refer to specific database engines.

+   - The DBD (database driver) level provides support for various database engines by means of drivers that are engine specific. The DBD-level module that implements DBI support for MySQL is named DBD::mysql.

The DBI architecture enables you to write applications in relatively generic fashion. When you write a DBI script, you use a standard set of database-access calls. The DBI layer invokes the proper driver at the DBD level to handle your requests, and the driver handles the specific issues involved in communicating with the particular database server you want to use. The DBD level passes data returned from the server back up to the DBI