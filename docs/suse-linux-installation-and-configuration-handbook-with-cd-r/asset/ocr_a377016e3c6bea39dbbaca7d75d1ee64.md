# Configuration Files

The main configuration file for BIND 8.x is located in /etc/named.conf. You should be using this file primarily to get any of the name server types that are discussed in this chapter. As mentioned earlier, this book deals only with BIND version 8.x and not version 4.x. The configuration filename is different and there are differences in its formats.

> **CAUTION**
> This chapter does not discuss the setup of BIND version 4.x. BIND version 8.x is considered the default for SuSE Linux, starting with version 6.2. If you are upgrading from SuSE 6.1 to SuSE 6.2 or 6.3, you have to install BIND version 8.x manually or by using YaST. It does not get upgraded by default when you choose to update the existing system. You should consider upgrading this package because of the many security problems BIND 4.x has.

# The named.conf Statements

The named.conf file has a unique syntax that is easy to understand. The file is made up of comments, statements, and sub-statements (sub-statements are blocks of statements from the main statements):

Comments—The comment style in the named.conf file can be any of the following:

+   - C style—/* This is a C style comment*/
+   - C++ style—//This is a C++ one line style comment
+   - Shell style—#This is a shell one line style comment

> **CAUTION**
> The semicolon (;) is not considered a comment. Semicolons are used to terminate a statement. Watch out for errors caused by semicolons.

Main Statements—Every statement should end with a semicolon (;). The following statements are supported by BIND:

+   - acl—This statement must be used to create a name address match list. Before using this statement, you have to define a match list name in order for acl to use it.
+   - include—Includes another configuration file at the point where this statement appears. It is considered a good style if you cut the configuration file in more than one piece to have control over them.
+   - key—To use the server definition, you must create a key ID for it using the key statement. The key statement creates a special key that stores associated information for authentication methods for a specified name server.