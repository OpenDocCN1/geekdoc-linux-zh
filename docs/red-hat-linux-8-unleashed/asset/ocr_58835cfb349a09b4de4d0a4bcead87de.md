# CHAPTER 18 Secure File Transfer Protocol (FTP) Service

These files are installed in the /etc directory by the RPM package. The following sections describe each of these files and how to use the commands they contain to configure the Red Linux Wu-FTP server.

> CAUTION
When configuring an anonymous FTP server, it is extremely important to ensure that all security precautions are to prevent malicious users from gaining privileged level access to the server. Although this chapter shows you how to configure your FTP server for secure use, all machines connected to the Internet are potential targets for malicious attacks. Vulnerable systems can be a source of potential liability, if anyone accesses and uses them to store local copies of proprietary software—even temporarily. There is little value in configuring a secure FTP if the rest of the system is still vulnerable to attack. Use Red Hat's lokkit or redhat-config-securitylevel client to implement a firewall on your system.

> TIP
Whenever editing the FTP server files, make a backup file first. Also, it's always a good idea to comment out (using a pound sign at the beginning of a line) what is changed instead of deleting or overwriting entries. Follow these changes with a brief description what the change was. This makes a neat audit trail of what was done, by whom, when, and why. If you have any problems with the configuration, these comments and details will help you troubleshoot and return to valid entries if necessary. You can use the rpm command or Linux tools (such as mc) to extract a fresh copy of a configuration file from the software's RPM archive. Be aware, however, that the extracted version will replace the current version and overwrite your configuration changes.

> NOTE
Back up the FTP server configuration files to another machine, should any of the working copies become corrupt. There might be a need to replicate server configurations across multiple hosts or revert back to an original copy of the defaults at some point in time. By making regular backups before changing a file, you guarantee that the changes can be undone and a working server restored with minimal down time.

# Using Commands in the ftpaccess File to Configure wu-ftpd

The ftpaccess file contains most of the server configuration details. Each line contains a definition or parameter that is passed to the server to specify how the server is to operate. The directives can be broken down into the following categories, including

+   - Access Control—Settings that determine who can access the FTP server and how it is accessed