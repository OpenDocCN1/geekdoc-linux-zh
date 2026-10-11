# # Limiting Users

**Objective 1.14 Security**  
- Setup user level security. Set limits on user logins, processes, and memory usage

One type of security violation is known as a *denial-of-service (DoS)* attack. These attacks are caused by malicious users using an excessive amount of resources so that others cannot legitimately use the system. To stop some attacks, you can limit your users to certain constraints. This is done with the `/etc/security/limits.conf` file. The format for this file is as follows:

```
<domain> <type> <item> <value>
```

The *domain* can be set to a user name, a group name (*@group*), or an *\** for every-one. The *type* field designates the type of limit this is, hard or soft. Table 17-19 lists the items that can be limited. The *value* field sets the limit amount.

Table 17-19  
Items

| **Limit** | **Description** |
| --- | --- |
| *core* | Limits the core file size, in K |
| *data* | Limits the maximum data size, in K |
| *fsize* | Limits the maximum file size, in K |
| *memlock* | Limits the maximum amount of locked-in-memory address space, in K |
| *nofile* | Limits the maximum number of open files. |
| *rss* | Limits the maximum resident set size, in K |
| *stack* | Limits the maximum stack size, in K |
| *cpu* | Limits the amount of CPU time given to the user, in minutes. |
| *nproc* | Limits the maximum number of processes. |
| *as* | Limits the address space. |
| *maxlogins* | Limits the maximum number of logins for this user. |
| *priority* | Sets the priority to run user processes at. |

Take the following example:

```
#<domain> <type> <item> <value>
```