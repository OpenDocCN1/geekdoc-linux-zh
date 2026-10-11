# **The acl statement**

The *access control list* (ACL) statement must be at the top of the configuration file, but the `name_of_acl` created can be used anywhere that an address match list is used. The syntax is as follows:

```
```
acl name_of_acl {
    Address_match_list
};
```
```

The `acl` statement should be at the top of your configuration file. The ACL name defined in the block cannot be used before the `acl` block is encountered. Table 16-27 lists four predefined ACL lists.

| Table 16-27 | | 
| Predefined ACL Lists | |

| List | Members |
|---|---|
| Any | Allow all hosts. |
| None | Deny all hosts. |
| Localnets | Allow local networks off any interface on the system. |
| Localhost | Allow the IP of any interface on the system. |

# **The server statement**

The `server` statement lets you define certain characteristics for remote servers. The possible characteristic settings are shown in Table 16-28. The syntax is as follows:

```
```
server ip_addr {
    [ bogus yes_or_no; ]
    [ support-ixfr yes_or_no; ]
    [ transfers number; ]
    [ transfer-format ( one-answer | many-answers ); ]
    [ keys { key_id [key_id ... ] }; ]
};
```
```

| Table 16-28 | |
| server Statements | |

| Statement | Function |
|---|---|
| bogus yes \| no; | If set to yes, no queries are sent to the server. This can be useful to temporarily stop queries going to a server that is giving out incorrect information. |