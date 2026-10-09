NIS (Network Information Service) simplifies the maintenance of common administrative files by keeping them in a central database and having clients contact the database server to retrieve information from the database. Developed by Sun Microsystems, NIS is an example of the client/server paradigm.

Just as DNS addresses the problem of keeping multiple copies of/etc/hosts files up-to-date, so NIS deals with the issue of keeping system-independent configuration files (such as /etc/passwd) current. Most networks today are heterogeneous (page 1253); even though they run different varieties of UNIX or Linux, they have common common attributes, such as a passwd file.

An LDAP (Lightweight Directory Access Protocol) directory can hold many types of information, including names and addresses, lists of network services, and authentication data. Another example of the client/server paradigm, LDAP is appropriate for any type of relatively static, structured information where fast lookups are required. Many types of clients are set up to communicate with LDAP servers, including email clients, browsers, and authentication servers.

# ## INTRODUCTION TO NIS

A primary goal of a LAN administrator is to make the network transparent to users. One aspect of this transparency is presenting users with similar environments, including usernames and passwords, when they log in on different machines. From the administrator's perspective, the information that supports a user's environment should not be replicated but rather should be kept in a central location and distributed as required. NIS simplifies this task.

As with DNS, users need not be aware that NIS is managing system configuration files. Setting up and maintaining NIS databases are tasks for the system administrator; individual users and users on single-user Linux systems rarely need to work directly with NIS.

Yellow Pages NIS used to be called the Yellow Pages, and some people still refer to it by this name. Sun renamed the service because another corporation holds the trademark to the Yellow Pages name. The names of NIS utilities and files, however, are reminiscent of the old name: ypcat displays and ypwhich searches an NIS file, and the server daemon is named ypserver.

# ## HOW NIS WORKS

No encryption NIS does not encrypt data it transfers over the network—it transfers data as plaintext.

NIS domain NIS makes a common set of information available to systems on a network. The network, referred to as an NIS domain, is characterized by each system having the same NIS domain name (different than a DNS domain name [page 1247]). Technically an NIS domain is a set of NIS maps (database files).