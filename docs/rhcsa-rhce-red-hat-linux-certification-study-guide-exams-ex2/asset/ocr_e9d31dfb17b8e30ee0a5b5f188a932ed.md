# The Secure Shell Package

+   - SSH server configuration commands include sshd, ssh-agent, ssh-add, ssh-keygen, ssh-copy-id, and ssh.
+   - SSH server configuration files in the /etc/ssh directory include client and server configuration files, along with public and private host keys, encrypted with RSA and DSA formats.
+   - User home directories include their own .ssh subdirectory of configuration files, with private and public identification keys, suitable for passphrases.
+   - Private/public keypairs can be configured with passphrases with the ssh-keygen command.
+   - Public keys can be transmitted to the home directory on remote systems with the ssh-copy-id command.
+   - The SSH server configuration file, sshd_config, can be set up with user-based security.
+   - The easiest way to set up host-based SSH security is through TCP Wrappers.

# A Security and Configuration Checklist

+   - You'll need to install a number of services to prepare for the RHCE exam, with commands like rpm and yum.
+   - One way to make sure services survive a reboot is with the chkconfig command; a full list of such commands related to RHCE services are listed in the chapter.
+   - You'll need to configure access to a service through layers of security, including SELinux, iptables-based firewalls, and TCP Wrappers.