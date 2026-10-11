# IN THIS APPENDIX

+   * Encryption ............... 1044
+   * File Security ............... 1049
+   * Email Security ............... 1049
+   * Network Security ............... 1050
+   * Host Security ............... 1053
+   * Login Security ............... 1054
+   * Remote Access Security ............... 1055
+   * Viruses and Worms ............... 1056
+   * Physical Security ............... 1056
+   * Security Resources ............... 1058

# C

# # SECURITY

Security is a major part of the foundation of any system that is not totally cut off from other machines and users. Some aspects of security have a place even on isolated machines. Examples of these measures include periodic system backups, BIOS or power-on passwords, and self-locking screensavers.

A system that is connected to the outside world requires other mechanisms to secure it: tools to check files (**tripwire**), audit tools (**tiger** / **cops**), secure access methods (**kerberos** / **ssh**), services that monitor logs and machine states (**swatch** / **watcher**), packet-filtering and routing tools (**ipfwadm** / **iptables** / **pchains**), and more.

System security has many dimensions. The security of your system as a whole depends on the security of individual components, such as your email, files, network, login, and remote access policies, as well as the physical security of the host itself. These dimensions frequently overlap, and their borders are not always static or clear. For instance, email security is affected by the security of files and your network. If the medium (the network) over which you send and receive your email is not secure, then you must take extra steps to ensure the security of your