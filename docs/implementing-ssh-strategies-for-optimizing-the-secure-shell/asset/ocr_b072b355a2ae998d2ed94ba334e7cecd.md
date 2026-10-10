![](bbox=[0.16, 0.08, 0.61, 0.4])

Figure 2.26  Logging section from the VShell server.

# Comparison of OpenSSH, SSH Server, and VShell

The SSH servers discussed in this chapter have similar functionality, but significant differences exist among them. For example, VShell SSH server offers easy configuration methods to restrict shell access to an SSH client but also allows other SSH options such as SFTP or port forwarding. If SSH needs to be set up for secure file transfer, shell access should probably be restricted. If VShell is used, this restriction can be set quite easily. On the other hand, OpenSSH does not offer quite the same ease of restricting shell access to users. Similarly, if SSH needs to be set up for remote management to internal servers only, all three SSH servers can be used; however, if remote management needs to be limited to a specific number of machines and ports, VShell and SSH Communications’ are probably good choices, since they offer SSH access with port-forwarding restrictions.

If SSH is being deployed in an environment where several different SSH servers exist, OpenSSH is probably a good choice, since it offers the most flexibility and interoperability with any other SSH server that may be a different installation.

Your choice of an SSH server is highly dependant on the type of functionality required for SSH. Because SSH can be used in a variety of ways, you need to understand the different servers and the specific functionality that each offers.