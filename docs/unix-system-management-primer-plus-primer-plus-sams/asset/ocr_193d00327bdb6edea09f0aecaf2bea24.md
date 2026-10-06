# 412 UNIX SYSTEM MANAGER PLUS PRIME

FIGURE 14.3
A functionality matrix in an Excel spreadsheet.

![](bbox=[0.315, 0.055, 0.945, 0.415])

Maintaining your host functionality documentation in a relational database such as Oracle or MySQL provides even more convenience. You can query the database for exactly the informa you want to see about your services, and even cross-reference your query with other data in the database.

If you included the IP addresses of each server in the functionality matrix, for example, could you query for a list of services that would be affected if the 172.16.5.0/24 were unreachable; the database would provide an immediate response. Querying for functional dependencies saves a significant amount of time when you are planning for maintenance or reviewing system vulnerabilities. One such query might look like this:

```
SQL> select service from functionality_matrix where network = 172.16.5.0;
```

```
SERVICE
----
authoritative DNS
mail hub
corporate web server
```

# Procedural Documentation

The bulk of documentation that a system administrator produces is procedural in nature; procedural documentation describes the step-by-step processes for performing daily operational tasks. Some examples of this kind of documentation include instructions for the following: