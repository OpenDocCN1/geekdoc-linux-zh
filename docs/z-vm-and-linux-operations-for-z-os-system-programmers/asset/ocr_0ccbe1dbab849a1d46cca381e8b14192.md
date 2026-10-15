+   - Personal computer-based graphics
+   - TCP/IP performance reporting

In addition to analyzing VM performance data, the Performance Toolkit processes Linux performance data obtained from the Resource Management Facility (RMF™) Linux modular data gatherer, rmfpm s. The gathered data can be analyzed using the RMF PM client application. The Linux performance data obtained from RMF can be viewed and printed in a manner similar to the presentation of VM data.

The rmfpm s application is available from the following site:

```
http://www.ibm.com/servers/eserver/zseries/zos/rmf/rmfhtmls/pmweb/pmlin.html
```

> z/OS analogy: The application is similar to RMF MONITOR in z/OS.

# 2.3.16 RACF Security Server for z/VM

The Resource Access Control Facility (RACF) Security Server for z/VM is a security tool that works together with existing functions in the z/VM base system to provide improved data security for an installation. RACF protects information by controlling access to it.

RACF also controls what you can do on the operating system and protects your resources. It provides this security by identifying and verifying users, authorizing users to access protected resources, and recording and reporting access attempts.

To help each installation meet its unique security requirements and objectives, RACF provides:

+   - Flexible control of access to protected resources
+   - Ability to store information for other products
+   - Choice of centralized or decentralized control profiles
+   - Transparency to users
+   - Exits for installation-written routines

Your organization can define individuals and groups who use the system that RACF protects. A security administrator uses RACF to define a profile for each individual that identifies that person's user ID, password, and other information.