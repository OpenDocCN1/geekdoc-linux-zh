| Profile Name | Command | Attributes |
|---|---|---|
| All | * | |
| Audit Control | /etc/init.d/audit | euid=0;egid=3 |
| Audit Control | /etc/security/bsmonconv | uid=0 |
| Audit Control | /etc/security/bsmunconv | uid=0 |
| Audit Control | /usr/sbin/audit | euid=0 |
| Audit Control | /usr/sbin/auditconfig | euid=0 |
| Audit Control | /usr/sbin/auditd | uid=0 |
| Audit Review | /usr/sbin/auditreduce | euid=0 |
| Audit Review | /usr/sbin/praudit | euid=0 |
| Audit Review | /usr/sbin/auditstat | euid=0 |
| Printer Management | /etc/init.d/lp | euid=0 |
| Printer Management | /usr/bin/cancel | euid=0 |
| Printer Management | /usr/bin/lpstat | egid=14 |
| Printer Management | /usr/bin/enable | euid=lp |
| Printer Management | /usr/bin/disable | euid=lp |
| Printer Management | /usr/sbin/accept | euid=lp |
| Printer Management | /usr/sbin/reject | euid=lp |
| Printer Management | /usr/sbin/lpadmin | egid=14 |
| Printer Management | /usr/sbin/lpfilter | euid=lp |
| Printer Management | /usr/sbin/lpforms | euid=lp |
| Printer Management | /usr/sbin/lpmove | euid=lp |
| Printer Management | /usr/sbin/lpshut | euid=lp |
| Printer Management | /usr/sbin/lpusers | euid=lp |

![](bbox=[0.122, 0.707, 0.221, 0.774])

Be familiar with the formats of all four RBAC database files and the purpose of each field.

# Managing the RBAC

You can use the following commands to manage RBAC:

+   - **auths(1)**—Displays authorizations assigned to a user account
+   - **profiles(1)**—Displays profiles assigned to a user account