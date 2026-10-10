# # Linux Hacking



# ## Objectives

After completing this chapter, you should be able to:

+   * Identify basic commands and features of Linux
+   * Identify the Linux file structure
+   * Know how to use the Linux kernel
+   * Know how to compile programs in Linux
+   * Describe Linux security
+   * Describe common Linux vulnerabilities
+   * Explain Linux IPTables
+   * Explain SARA
+   * Explain Linux rootkits
+   * Apply rootkit countermeasures
+   * Describe Linux intrusion detection systems
+   * Use tools in Linux

# ## Key Terms

**Alias**	a custom command in Linux that is a substitute for a formal command string; for example, if a user prefers to always see the long listing of a directory, he or she can set up an alias so that typing ll on the command line aliases to ls -l. The danger for security is if an attacker aliases commands at the root level, overwriting the behavior of common commands.

**Chmod**	the UNIX/Linux command for changing permissions; permissions are grouped by population (owner, group, world) and access (read, write, execute)

**Chroot**	a security measure in Linux that changes the root folder of a root process to one part of the system; with chrooting, the root process is restricted to one directory tree, which is called a chroot "jail"

**Firewall**	software that is written to provide security between the system and the network