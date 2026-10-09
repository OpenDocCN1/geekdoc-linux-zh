# **SetEnvIfNoCase**

The `SetEnvIfNoCase` directive is the same as `SetEnvIf`, except that it offers case-insensitive regular expression matches.

**Syntax:** `SetEnvIfNoCase attribute regex variable=value [...]`

**Context:** Server config

# **mod_unique_id**

The `mod_unique_id` module provides a magic token for each request that is guaranteed to be unique across “all” requests under very specific conditions. The unique identifier is even unique across multiple machines in a properly configured cluster of machines. The environment variable `UNIQUE_ID` is set to the identifier for each request. There are no directives for this module.

# # Authentication and Access Control Modules

Apache has a number of modules to perform authentication and authorization tasks. In most cases, the authentication modules use basic HTTP authentication, which uses plain text passwords. The authorization module allows you to control access to a directory of your Web site via a username or IP address. The modules shown in Table 5-2 enable you to perform authentication and access control tasks.

| Table 5-2 | Authentication and Access Control Modules |
| --- | --- |
| **Module** | **Purpose** |
| mod_auth | This is the standard authentication module, which implements Basic HTTP authentication. See Chapter 7 for details. |
| mod_auth_anon | Gives anonymous user access to authenticated areas. |
| mod_auth_dbm | Provides user authentication using DBM files. |
| mod_auth_db | Provides User authentication using Berkeley DB files. |
| mod_auth_digest | This module implements Digest authentication using Message Digest 5 (MD5). |
| mod_access | This module allows you to authorize access by using host name or IP address. See Chapter 7 for details. |