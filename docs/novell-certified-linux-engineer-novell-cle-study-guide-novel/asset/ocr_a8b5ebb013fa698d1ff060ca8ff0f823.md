# # eDirectory and LDAP

Test Objectives Covered:

+   - Describe how eDirectory works.
+   - Perform eDirectory administration tasks.

The version of eDirectory that is installed with NNLS includes a very powerful LDAP server. LDAP is a set of standards that provides controlled access to the information stored in a directory such as eDirectory.

Before we go any further, we need to make some clarifications about the nature of LDAP. The concept of LDAP tends to confuse a lot of people, even those who have a lot of experience with directory services.

LDAP, as stated earlier, is a protocol that allows programmers to write applications that can read and write information to a directory service that complies with the X.500 directory standard (hence the name Lightweight Directory Access Protocol).

LDAP is not, as many think, a directory service in and of itself. The confusion comes because we use the term *LDAP server* frequently in the industry. A more correct term would be *LDAP service*. The LDAP server doesn't contain any information, such as containers or objects. It simply allows you to access information in an LDAP-compliant directory service, such an eDirectory. This is shown in Figure 5.35.

![](bbox=[0.3, 0.61, 0.6, 0.76])

The goal behind the LDAP protocol is to provide a common way to access directory information. As shown in Figure 5.35, programmers can access system information in a directory with either the native directory access protocols established by the vendor with LDAP calls.

Without LDAP, programmers would have to learn a whole new API set for each directory service they needed to write applications for. With LDAP, they can learn a single set of protocols and use it with many different directory services.