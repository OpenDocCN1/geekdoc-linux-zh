Use a password creation methodology. Think of a memorable phrase such as “Way down upon the Suwanee river, Far, far away.” Next, turn it into an acronym including the punctuation. For example, **WdutSr.Fa**. Increase the complexity by substituting numbers for some letters. Be consistent, replacing certain letters with the same numbers; for example, replace d with 6, F with 7, and so on, giving you a finished password of **W6ut5r.7.fa**.

One good password protection policy is password aging. Password aging means that a password will remain valid for a set amount of time, then the user will be prompted to change the password. Aging also can ensure that the same password cannot be reused and require that it be active for a number of days before it can be changed.

Red Hat Linux provides several ways to authenticate and to ensure that passwords are protected from unauthorized access. The Authentication Configuration screen, shown in Figure 3–23, provides the options to accomplish this. The following is a brief description of each option:

FIGURE 3–23
Red Hat authentication configuration.

![](bbox=[0.26, 0.3, 0.82, 0.58])

+   * **Use Shadow Passwords** enhances the security of system authentication files by moving encrypted password hashes from the clear-text /etc/passwd file to /etc/shadow, which is readable only by the root user. Shadow passwords also store information about password aging and allow enforcement of security policies.
* **Enable MD5 Passwords** allows a long password to be used, up to 256 characters instead of eight.
* **Enable NIS** allows you to run a group of computers in the same Network Information Service domain with a common password and group file.
* **Enable LDAP**, Lightweight Directory Access Protocol, is a centralized hierarchical database used for authentication.
* **Enable Kerberos** is a secure system for providing network authentication services.

For your installation select **Use Shadow Passwords** and **Enable MD5 Passwords**, as shown in Figure 3–22. These options will render the passwords unreadable by most users and allow for lengthy passwords.

# Objective 1.5
Packages

After you have configured and formatted your partitions, you are ready to select packages for installation. Packages are applications that can be installed on your Red Hat Linux installation to accomplish a wide range of tasks. For example, packages can be installed to