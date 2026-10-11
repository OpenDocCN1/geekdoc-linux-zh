# # Multi-Category Security in SELinux in Fedora Core 5

## How to set up and use SELinux Multi-Category Security.

RUSSELL COKER

The release of Fedora Core 5 added several new features to SELinux, one of which is Multi-Category Security (MCS). The purpose of MCS is to protect data confidentiality, which means it will prevent secret data from being exposed, but it is not designed to prevent the system from being cracked. The SELinux functionality that you may be familiar with from previous Fedora releases (known as the domain-type model) is still used for protecting system integrity. MCS is an extra feature for preventing accidental or deliberate leaks of secret data.

Earlier releases of SELinux used only the domain-type model for access control. In the domain-type model, every process has a domain, and every object that a process may access (files, directories and so on) has a type. The system maintains a set of rules to specify which types each domain may access and what type of access should be.

Although domain-type can be used to implement all controls of system integrity and data confidentiality (and has been used for this in the past), it makes for a cleaner design if the goals of integrity and confidentiality are separated. MCS is designed to protect data confidentiality, thus allowing the domain-type part of the policy to be focused on protecting system integrity. MCS is based on some of the design features of Multi-Level Security (MLS). MLS is designed for military use and is not suitable for most users, so I don’t cover it in this article.

In the past, MLS has had little support, because it’s difficult to use and expensive. MCS is a default feature in Fedora Core 5 and above, so it will have good support by application developers and system administrators. It is expected that all applications written for Fedora Core 5 and above will have support for MCS, and that, in most cases, the MCS support also will allow those applications to support MLS. This means organizations that need the MLS features will have a better choice of applications than they would on a proprietary UNIX system.

MCS adds a sensitivity label (which I refer to as an MCS label for the rest of this article) to each security context. The security context is the complete SELinux label for a process or a resource that a process may access. To access a file, a process must have an MCS label that dominates the MCS label of the file to be accessed. The MCS label is composed of a set of categories. A process may have an MCS label with two levels, referred to as high and low level; the high level has a super-set of the categories of the low level.

A file might have the MCS label s0: c0: c10. The s0 means nothing in the MCS policy, that field is used by the MLS policy, and the same kernel code is used for both MLS and MCS, so the format can’t be changed. The part that matters is c0: c10, which means the set of categories from c0 to c10 inclusive (the \_ character indicates a range of categories). In Fedora Core 5, there are 256 categories numbered from c0 to c255. In Fedora Core 6, there will be 1,024 categories numbered from c0 to c1023.

A process might have the MCS label s0: c0: c100, which means that the low level of the label (or range) is s0 (no categories) and the high level is s0: c0: c100, which means all categories from c0 to c100. Disjoint sets of categories also are permitted. The label s0: c3, c5 +c3: c5- c5- c0: c10, c20: c30 means that the low level has categories c3 and c5, while the high level contains categories c0 to c10 inclusive and c20 to c30 inclusive.

Categories must be named, and it is expected that most users will name all the categories that are used. In Fedora Core 5, you have to edit the file /etc/selinux/targeted/setrans.conf to change the human-readable names for the MCS labels. Below is a section of the default setrans.conf file: