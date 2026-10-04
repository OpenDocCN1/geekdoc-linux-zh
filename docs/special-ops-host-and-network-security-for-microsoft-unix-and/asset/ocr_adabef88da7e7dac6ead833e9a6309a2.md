# Chapter 1 • Assessing Internal Network Security

comprehensive in your assessment of some, while only gathering the high-severity vulnerabilities from other networks. Each of these solutions can be performed using the tools and techniques detailed in each chapter, using the techniques described in Chapter 3, or using an automated vulnerability assessment product.

# Using an Automated Vulnerability Assessment (VA)

Vulnerability assessment (VA) is a term for applications that automate the process of vulnerability assessment. They allow you to check many machines in the time it would take to interrogate a few manually. All VA tools will perform host discovery and detect live systems to scan on the network. They all have some service discovery (port scanning) or low-level enumeration feature to determine which services are active and need to be checked on each host. Finally, perform vulnerability checking to determine if the active service has any security issues. VA is a critical piece of the INS lifecycle, however, it does not remove the human element entirely.You should do manual system checks to verify false positives in the report as perform host reviews to identify false negatives.

# Performing Host Diagnostic Reviews

Assessing the security of individual hosts can be very valuable once you have covered the basics, such as finding common network vulnerabilities. A host assessment will uncover vulnerabilities that would never be found during a standard host and network assessment. Some key areas to review include the following:

+   - OS patch management
- File system security (including Registry for Windows)
- User accounts
- Passwords
- File sharing (Network File System [NFS] or Windows sharing
- Active services
- TCP/IP host filtering
- Logging and auditing
- OS-specific security settings