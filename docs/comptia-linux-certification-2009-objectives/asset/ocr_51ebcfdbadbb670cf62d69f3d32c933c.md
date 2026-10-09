![](bbox=[0.4, 0.09, 0.9, 0.32])

*Figure 13-4: Configuring a directory to recognize CGI scripts.*

# ## Syntax for Renaming the .htaccess File

The .htaccess file can be renamed using the **AccessFileName** directive where the syntax is: **AccessFileName new file name**.

# ## The order Statement

The order statement, which is included in the **mod\_access** module, provides the access control for a system. It operates along with the **Allow** and **Deny** directives. It involves three passes. In the first pass, it processes all the **Allow** or **deny** directives based on their specification. In the second pass, it processes the directive other than the first pass directive. In the third pass, it processes the requests that do not match either the **Allow** or **Deny** directives.
The syntax is:

```
```
Order Ordering Allow|from hostname|IP address or the IP address range
Deny from hostname|IP address or the IP address range
```
where the ordering value is set to either "Allow, deny" or "Deny, allow".
```

# # The apachectl Command

The Apache HTTP Server Control Interface (**apachectl**) is the interface that allows an administrator to control the functioning of the HTTP service using the **apachectl** command. The **apachectl** command supports various options.

![](bbox=[0.05, 0.65, 0.2, 0.73])

| Option | Used To |
| --- | --- |
| start or apachectl -k start | Start the apache daemon. If the daemon is already running, it displays an error message. |
| stop or apachectl -k stop | Stop the apache daemon. |
| restart or apachectl -k restart | Restart the apache daemon. If the daemon is not running, it starts the daemon. |
| fullstatus | Display the full status report of the services running and requested by clients. It requires the mod_status module to be enabled on the system. |