Lightweight Directory Access Protocol (LDAP) LDAP provides data-bases that can be used to store arbitrary information, including informa-tion on user accounts and other information of the sort maintained by NIS. LDAP is generally considered more secure than NIS.

Pluggable Authentication Module (PAM) Facility The PAM facility is a Red Hat Linux facility that lets configure security-related options of PAM-aware programs. For example, you can use the PAM facility to tai-lor policies that restrict the form of valid passwords. PAM configura-tions for PAM-aware programs reside in /etc/pam.d.

# Key Terms

Before going on to the next chapter, be sure you're familiar with the follow-ing terms:

+   - key
- LDAP
- maps
- NIS
- PAM
- TCP wrappers

# Additional Sources of Information

For further information on restricting access to primary network services, we:

+   - The LDAP documentation, /usr/doc/ldap-*, and the LDAP Web site, www.openldap.org
- NET-3-HOWTO, by Terry Dawson and Alessandro Rubini, /usr/doc/HOWTO/NET-3_HOWTO
- NIS HOWTO, by Thorsten Kukuk, /usr/doc/HOWTO/NIS-HOWTO
- The PAM documentation files, /usr/doc/pam-*