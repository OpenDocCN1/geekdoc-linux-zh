For more information about maintaining the z/VM user directory, refer to:

+   - z/VM: CP Planning and Administration, SC24-6083
+   - z/VM:CP Commands and Utilities Reference, SC24-6081

# Security products

In earlier days, defining users to TSO would imply defining them in the User Attribute Data Set (SYS1.UADS) using the ACCOUNT command. By now, most installations have merged this data set into their RACF data base or similar for ISV products. When UNIX System Services were introduced in OS/390®, it became almost impossible to run a z/OS system without having a security system like RACF or similar activated. As several of the basic system functions of z/OS, for instance TCP/IP, are using or exploiting UNIX System Services, it is very difficult to operate without a security server of some sort. Even some of the installation material states that it is a prerequisite that the user responsible for installing z/OS should have access to different resource classes and similar. Without a security product, the standard modules or services performing these checks (SAF) would most certain fail these services.

The UADS (or RACF data base or both) contains data on every TSO user (the RACF base also contains STC and batch idents and other security related data). The base contains the user ID, the associated password, account number or code, the default procedure name and all attributes for each user. Most installations probably implement some kind of grouping or role-based security based on their business. For instance, all system programmers are typically members of the same group defined to RACF, to simplify management of access rules if such grouping has been implemented.

The base itself is stored in an encrypted format, so passwords and other data cannot be retrieved from the base directly. This also applies to independent software vendor (ISV) alternatives.

# A typical process for defining users in z/OS

A typical set of tasks necessary to define a TSO, STC, or batch user in z/OS includes establishing rules for the following areas:

| Security product | Users have to be defined to the security server or product, such as RACF. |
| Storage management | Rules for how to manage the user's data have to be addressed. This could involve adjustment of storage management services (SMS) constructs, defining catalog aliases, preallocating ISPF profiles, and so on. |
| Other | Several sites are also doing various tailoring for their TSO users, such as adjustment of TSO/ISPF JCL procedures or related services. Accounting might also |