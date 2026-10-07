# The K Command Type Argument

type is the database type. Several database types were discussed in Chapter 6 in relationship to which compiler options add support for which database types. The long list of database types discussed in Chapter 6, however, is only part of the story. Sendmail has several internal database types. Table 7.1 lists all of the valid type values.

Table 7.1 Valid K Command Type Values

| Type | Description |
| --- | --- |
| arith | An internal routine for doing arithmetic. |
| btree | A type added by the NEWDB compiler option. |
| bestmx | An internal routine that retrieves the MX record for a host. |
| dbm | A type added by the NDBM compiler option. |
| dequote | An internal routine that removes quotation marks. |
| dns | An internal routine that retrieves the address record for a host name. |
| hash | A type added by the NEWDB compiler option. |
| hesiod | A database located on a hesiod server. |
| host | An internal table for hostnames. |
| implicit | The type used for the aliases database file. |
| ldap | A database located on an LDAP server. |
| netinfo | A database located on a NeXT netinfo server. |
| nis | A database located on an NIS server. |
| nisplus | A database located on an NIS+ server. |
| null | An internal routine that returns "Not found" for all lookups. |
| ph | A database located on a CCSO Nameserver. |
| program | Passes the query to an external program. |