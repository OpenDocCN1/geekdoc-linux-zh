# The include Statement

The **include** *statement* is used to specify the file name that needs to be included in the named.conf file. The **include** keyword is followed by the file path. Any confidential information, such as a key’s description, can be provided in a separate file instead of specifying it in the named.conf file.

![](bbox=[0.03, 0.2, 0.75, 0.3])

*Figure 12-36: Adding a file using the include statement.*

# Syntax

The syntax of the **include** statement is *include “file name”;*

# The options Statement

The *options* *statement* is used to define the global server configuration, such as the location of the named utility, and the type of queries that can be allowed. This statement is also used to set default values for other statements. The **options** keyword is followed by a set of options enclosed within curly braces and should end with a semicolon ( ; ).

![](bbox=[0.03, 0.52, 0.75, 0.64])

*Figure 12-37: The use of the options statement.*

There are many options that can be provided in the *options* statement. Some of the frequently used options are listed in the table.

| Option | Description |
| :--- | :--- |
| *allow-query* | Specifies the hosts that are allowed to query the name server. By default, all hosts are permitted to query the name server. The *allow-query* option can have an ACL name or a collection of IP addresses. |
| *allow-recursion* | Specifies the hosts that are allowed to perform recursive queries on the name server. By default, all hosts are permitted to perform recursive queries on the name server. |