corresponding execute bit is also set. For example, if the sticky bit is set but the world's execute bit is not set, a symbol T is displayed instead of t. Table 6.9 summarizes the special mode symbols displayed depending on the execute bit setting.

**TABLE 6.9**  
**Special Permission Textual Representation**

|  | EXECUTE BIT NOT SET | EXECUTE BIT SET |
|---|---|---|
| SUID | `---S------` | `---s------` |
| SGID | `------S---` | `------s---` |
| Sticky | `---------T` | `---------t` |

> **NOTE**
> 
> When you set these special permission modes using their textual values in chmod, use lowercase characters, such as s and t, and not the uppercase ones. The case distinction is used by ls to display the different permission combinations.

# Security Implications of SUID/SGID

It is worth discussing the need for SUID and SGID programs and scripts in the Linux/Unix world, even when they can be Trojan horses left behind by a hacker. First, consider the /etc/passwd file. Only the file owner (root) has write access (rw-r--r--) to it. Yet as an ordinary user, you can modify the contents of this file, albeit in a very limited way, using the passwd and chsh commands.

An examination of the permission bits of the /usr/bin/passwd program shows that both the SUID and execute bits are set (rwsr-xr-x) for the file owner. This indicates that the passwd utility is a root SUID program. It's a SUID program because of the s flag in the permission bits, and it's a root SUID program because root owns the file. Thus, when anyone runs the passwd program, the user temporarily gains the privileges of the root user—but only for the duration of the program's execution and only from within that program. Without such a mechanism, many system administration tasks can become unnecessarily complex due to the security implications. For instance, how would you effectively secure the /etc/shadow file and yet allow users to update their own passwords?

On the other hand, the SUID API call can be used to lower a user's privileges instead of increasing them. For instance, for an IP-based service to bind to one of the privileged ports, it needs to run as root. However, after the port is bound, the application no longer needs to have root privileges; it can use the SUID call to change the process's UID to that of a nonprivileged user. Or a