+   * rcp is used to copy files between systems.
+   * rsh is used to execute a single command on a remote system.
+   * rwho shows who is logged in on the local network.
+   * uptime shows the uptime of systems on the network.
+   * SSH is a secure replacement for the Berkeley r commands.
+   * sshd is the SSH server daemon.
+   * ssh is the SSH client used to log in to a remote system.
+   * scp is used to copy files between systems.
+   * sshd_config is the SSH server configuration file.
+   * ssh_config is the system-wide SSH client configuration file.
+   * ssh-keygen is used to create a user's identity keys.
+   * ssh-agent is used to hold keys so that a user needs to enter a passphrase only once.
+   * ssh-add adds a user's private keys to the agent.
+   * Shadow passwords store the encrypted password in /etc/shadow.
+   * Normal passwords are converted to shadow passwords using pwconv and grppconv.
+   * Shadow passwords can be converted back to normal passwords using pwunconv and grpunconv.
+   * Unneeded services should be removed to reduce security risks.
+   * The iptchains tool is used to set up firewall rules.
+   * The three default chains are Input, Output, and Forward.
+   * Rules are made up of conditions and targets.
+   * The first rule a packet matches is the only one applied.
+   * The six standard targets are ACCEPT, DENY, REJECT, MASQ, REDIRECT, and RETURN.
+   * IP masquerading lets you share one real IP address with many systems.
+   * PAM lets an administrator customize the authentication of some applications.
+   * The PAM configuration files are stored in /etc/pam.d.
+   * Security lists and sites should be monitored for new exploits.
+   * The /etc/security/limits.conf file can limit certain user items.
+   * The ulimit command can also limit some user items such as number of processes.
+   * Security tools should be used to detect problems and watch for file changes.