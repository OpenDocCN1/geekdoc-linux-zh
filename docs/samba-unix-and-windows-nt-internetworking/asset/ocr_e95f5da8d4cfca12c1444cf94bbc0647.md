unless the root preexec or root postexec parameters are used, which indicate that program execution will occur with root privileges. Carefully consider the application scope before using the root versions of these parameters. In most cases, alternatives can be found that produce the same results running under the calling user's privileges.

```
preexec = <command or script path name>
postexec = <command or script path name>
root preexec = <command or script path name>
root postexec = <command or script path name>
```

These parameters are useful tools for managing public resources. For example, preexec could be used to create and set the permissions for a personal work directory in a public lab. When the lab user disconnects from the share at logout time, postexec could be invoked to remove the work directory and execute other housecleaning activities like removing Web browser cookies, bookmarks, and other scratch files. Other uses for these parameters include presenting a system or informational message in a pop-up window when a share is accessed.

# Global Section

The [global] section of the smb.conf configuration file describes the roles the server will play in the workgroup or domain, defines default section parameter values, and sets limits and locations for administrative files and network options. Role information includes identification of the server's NetBIOS and workgroup names and, if the server will be acting as a WINS server, a master browser or a domain controller. Section defaults provide a means for reducing the repetition of parameter values in follow-on sections. These defaults can be explicitly overridden by assigning new values in individual sections when required.

The global section is something of a catchall for Samba functions and features that aren't clearly directed at a particular resource share definition. In Chapters 7–10 and Chapter 15, we'll look closely at some of the more complex function definitions that make up the global sections. These include authentication, name service, browsing, and domain configuration. For testing purposes, you might begin with some of the general parameter definitions listed in Example 6.3. A full set of global section parameters is listed in Table 6.4.

# Example 6.3 Sample Global Section Parameters

| Parameter | Description |
|---|---|
| netbios name = | Identifies server NetBIOS name |
| workgroup = | Identifies workgroup or domain |
| guest account = | User account used for guest access to to services marked "guest ok" |
| security = | Specifies whether login security is set to "user," "share," "server," or "domain" |