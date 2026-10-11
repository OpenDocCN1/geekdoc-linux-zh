# Table 5.1 Continued

| NNLS COMPONENT | DATA REQUIRED | DESCRIPTION |
|---|---|---|
| Virtual Office | eDirectory server IP address or hostname | This parameter specifies the IP address of the server where Virtual Office is to be installed. The server must be in the eDirectory tree and must host a Master or a Read/Write replica of a partition. |

|  | Admin name and context | This parameter specifies the admin user for the eDirectory tree. You must use a typeful name such as cn=admin,o=CLE. |

|  | Admin password | This parameter is the password for the admin user object you specified earlier. |

|  | NetStorage authentication server | This parameter specifies the IP address of the server that will be used to authenticate NetStorage users. This server must reside in the eDirectory tree and have LDAP installed. |

|  | NetStorage proxy user | At this prompt, you must supply the name of a user in the eDirectory tree that will be used to provide proxy access to the NetStorage service. In this book, we will simply use the tree admin. You must use a typeful name. |

|  | NetStorage proxy user password | This parameter supplies the password for the user specified earlier. |