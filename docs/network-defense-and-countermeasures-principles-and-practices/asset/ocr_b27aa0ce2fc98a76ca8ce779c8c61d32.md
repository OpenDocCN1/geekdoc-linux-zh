# CHAPTER 8 Operating System Hardening

are virtually impossible for users to remember. Many users will simply write the password on a note and keep it in a handy but insecure location, such as the top drawer of their desks, a security problem.

# Account Lockout Policies

When you open the Local Security Settings dialog, your options are not limited to setting password policies. You can also set account lockout policies. These policies determine how many times a user can attempt to log in before being locked out, and for how long to lock them out. Default Windows settings are shown in Table 8-3.

These default policies are not secure. They allow for an infinite number of log-in attempts, making the use of password crackers very easy and virtually guaranteeing that someone will eventually crack one or more passwords and gain access to your system. Table 8-4 provides the recommendations from Microsoft, National Security Agency, and the author.

# TABLE 8-3 Windows Default Account Lockout Policy Settings

| Policy | Default Settings |
|---|---|
| Account lockout duration | Not defined |
| Account lockout threshold | 0 invalid login attempts |
| Reset account lockout counter after | Not defined |

# TABLE 8-4 Recommended Account Lockout Policies

| Policy | Microsoft | NSA | Author |
|---|---|---||
| Account lockout duration | 0, indefinite | 15 hours | 48 hours. If someone is attempting to crack passwords on weekends/holidays, you will want the account locked until an administrator is aware of the attempt. |
| Account lockout threshold | 5 attempts | 3 attempts | 3 attempts |
| Reset account after | 15 minutes | 30 minutes | 30 minutes |

> FYI: More Guidelines

Guidelines for Windows Security are available on the following websites. These guidelines apply to all versions of Windows.
* National Security Agency: https://www.iad.gov/iad/library/ia-guidance/security-configuration/index.cfm
* Microsoft Guidelines: https://technet.microsoft.com/en-us/library/cc184906.aspx
Some of the lines in this chapter are long because they take you directly to the item in question. You can always go to the root domain (such as www.microsoft.com) and search for the item in question.
All of these sites provide other perspectives on securing a Windows client or server.