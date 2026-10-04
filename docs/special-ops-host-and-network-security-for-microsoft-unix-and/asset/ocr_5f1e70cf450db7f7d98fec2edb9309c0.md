# Chapter 14 • Attacking and Defending Unix

# Password Security

It is common knowledge that user passwords are the bane of the most secure configurations. A system can have the most rock-solid configuration in the world, yet fall to pieces because every user has a predictable password.

Like many other things in workstations, the security of passwords is a tradeoff. By forcing users to use passwords that are difficult to remember, the likelihood of forgotten passwords increases. By not enforcing password contents at all, the probability of dictionary attacks increase. To ensure that passwords are adequately secure, yet easy to remember, configure workstations to use password checking programs that notify a user when a password is too insecure. One example of such a program is pam_cracklib.so, a Pluggable Authentication Module (PAM) designed to check a password for ease of guessing or cracking.

# Platform-Specific Configurations

In the previous section, we discussed a number of general practices and procedures for securing servers and workstations. Because of the complexity of Unix systems, the roots of different Unix systems, and subtle variances that occurs between different flavors of the operating system, in this section, we highlight the major security features implemented with different platforms:

+   - Access Control Lists (ACLs)
- Role-Based Accounts
- Auditing
- Kernel Parameters
- Kernel Modules
- Service Configuration
- Host-based IDSs

Where possible, we also look at specific versions of Unix within a particular family, and discuss specific security features of operating systems within the family. This will include those of the commercial Unix family, the Berkeley Unix family, and the Linux family of operating systems. Where possible, we also add references to operating systems specific to each family. These operating systems may include Solaris, HP-UX, AIX, FreeBSD, and Red Hat Linux.