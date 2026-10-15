If the remote host can prove that it knows the corresponding private key (normally stored in /etc/ssh_host_key, a world-unreadable file), then sshd logs in the user without asking for a password.

Method B is more restrictive than method A, but we think it's still not quite secure enough. If the security of the originating host is compromised, the local site will be compromised as well.

+   - Method C: sshd can use public key cryptography to establish the user's identity. At login time, the user must have access to a copy of his or her private key file and must supply a password to decrypt it. The key can also be created without a password, which is a reasonable option for automating logins from remote systems.

This method is the most secure, but it's annoying to set up. It also means that users cannot log in when traveling unless they bring along a copy of their private key file (perhaps on a USB key, hopefully encrypted).

If you decide to use key pairs, make extensive use of ssh -v during the troubleshooting process.

+   - Method D: Finally, sshd can simply allow the user to enter his or her normal login password. This makes ssh behave very much like telnet, except that the password and session are both encrypted. The main drawbacks of this method are that system login passwords can be relatively weak if you have not beefed up their security, and that ready-made tools (such as John the Ripper) have been designed to break them. However, this method is probably the best choice for normal use.

Authentication policy is set in /etc/sshd_config. This file gets filled up with configuration rubbish for you as part of the installation process, but you can safely ignore most of it. The options relevant to authentication are shown in Table 22.2.

# Table 22.2 Authentication-related options in /etc/sshd_config

| Option | Meth' | Dft | Meaning when turned on |
|---|---|---|---|
| RhostsAuthentication | A | No | Obeys ~/.shosts, /etc/shosts.equiv, etc. |
| RhostsRSAAuthentication | B | Yes | Allows ~/.shosts et al., but requires host key |
| IgnoreRhosts | A,B | No | Ignores the ~/.rhosts and hosts.equiv files^a |
| IgnoreRootRhosts | A,B | No* | Prevents rhosts/shosts authentication for root |
| RSAAuthentication | C | Yes | Allows per-user public key authentication |
| PasswordAuthentication | D | Yes | Allows use of normal login password |

a. The authentication methods to which this variable is relevant
b. But continues to honor ~/.shosts and shosts.equiv
c. Defaults to the value of IgnoreRhosts