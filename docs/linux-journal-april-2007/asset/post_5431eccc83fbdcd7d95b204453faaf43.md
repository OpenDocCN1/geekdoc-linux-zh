
# Multi-Category Security in SELinux in Fedora Core 5

## How to set up and use SELinux Multi-Category Security.

RUSSELL COKER

The release of Fedora Core 5 added several new features to SELinux, one of which is Multi-Category Security (MCS). The purpose of MCS is to protect data confidentiality, which means it will prevent secret data from being exposed, but it is not designed to prevent the system from being cracked. The SELinux functionality that you may be familiar with from previous Fedora releases (known as the domain-type model) is still used for protecting system integrity. MCS is an extra feature for preventing accidental or deliberate leaks of secret data.

Earlier releases of SELinux used only the domain-type model for access control. In the domain-type model, every process has a domain, and every object that a process may access (files, directories and so on) has a type. The system maintains a set of rules to specify which types each domain may access and what type of access should be.

Although domain-type can be used to implement all controls of system integrity and data confidentiality (and has been used for this in the past), it makes for a cleaner design if the goals of integrity and confidentiality are separated. MCS is designed to protect data confidentiality, thus allowing the domain-type part of the policy to be focused on protecting system integrity. MCS is based on some of the design features of Multi-Level Security (MLS). MLS is designed for military use and is not suitable for most users, so I don’t cover it in this article.

In the past, MLS has had little support, because it’s difficult to use and expensive. MCS is a default feature in Fedora Core 5 and above, so it will have good support by application developers and system administrators. It is expected that all applications written for Fedora Core 5 and above will have support for MCS, and that, in most cases, the MCS support also will allow those applications to support MLS. This means organizations that need the MLS features will have a better choice of applications than they would on a proprietary UNIX system.

MCS adds a sensitivity label (which I refer to as an MCS label for the rest of this article) to each security context. The security context is the complete SELinux label for a process or a resource that a process may access. To access a file, a process must have an MCS label that dominates the MCS label of the file to be accessed. The MCS label is composed of a set of categories. A process may have an MCS label with two levels, referred to as high and low level; the high level has a super-set of the categories of the low level.

A file might have the MCS label s0:c0,c10. The s0 means nothing in the MCS policy, that field is used by the MLS policy, and the same kernel code is used for both MLS and MCS, so the format can’t be changed. The part that matters is c0,c10, which means the set of categories from c0 to c10 inclusive (the , character indicates a range of categories). In Fedora Core 5, there are 256 categories numbered from c0 to c255. In Fedora Core 6, there will be 1,024 categories numbered from c0 to c1023.

A process might have the MCS label s0:c0,c100, which means that the low level of the label (or range) is s0 (no categories) and the high level is s0:c0,c100, which means all categories from c0 to c100. Disjoint sets of categories also are permitted. The label s0:c3,c5 s0:c3,c5 s0:c0,c10,c20,c30 means that the low level has categories c3 and c5, while the high level contains categories c0 to c10 inclusive and c20 to c30 inclusive.

Categories must be named, and it is expected that most users will name all the categories that are used. In Fedora Core 5, you have to edit the file /etc/selinux/targeted/setrans.conf to change the human-readable names for the MCS labels. Below is a section of the default setrans.conf file:

```
# s0:c8=CompanyConfidential
# s0:c1=PatientRecord
# s0:c2=Unclassified
# s0:c3=TopSecret
# s0:c1,c3=CompanyConfidentialRedHat
s0:
s0-s0:c0,c255=SystemLow-SystemHigh
s0:c0=SystemHigh
```

And, the following is an example of how to use semanage to change the human-readable translations of MCS labels in Fedora Core 6:

```
# semanage translation -a -T ProjectA s0:c8
# semanage translation -l
```

| Level | Translation |
| :--- | :--- |
| s0 | |
| s0-s0:c0.c1023 | SystemLow-SystemHigh |
| s0:c0 | ProjectA |
| s0:c0.c1023 | SystemHigh |

Figure 1 shows the access that processes are granted to files for all combinations of the categories HR and financial.

MCS is designed with ease of use as a major concern. At the current time, its design is to control only file access. It also controls privacy (the system interface for strace, Tracer and debuggers) to prevent an unprivileged process from using a debugger to capture secret data from a more-privileged process.

The fact that MCS controls only file access does permit information leaks through filenames, and cooperating processes may use TCP, UDP, UNIX domain sockets or named pipes to transfer data. It was designed this way intentionally, because restricting all forms of inter-process communication will break many programs and make the entire system more difficult to use. The MLS policy (which is available in Fedora Core 5 and above but not enabled by default) restricts such communication methods, which is one of the reasons why it is regarded as being too difficult for most people to use.

When designing MCS, we decided not to try to prevent two cooperating users from inappropriately sharing data. We also decided not to prevent a user from reading a file with secret data and then writing that data to a file with a less secret label. Again, the MLS policy restricts these operations, but it is too difficult for most people to use.

![](img/3c4d8a97b5d96c835281dc0dacbc8551_62_0.png)

MCS and MLS are designed to protect confidentiality of data; they rely on the domain-type model to protect system integrity. FCS comes with three policies. The default is targeted, which offers much the same integrity protections as it did in FC4 but has the addition of MCS to protect data confidentiality. The next option is the strict policy, which, again, is much the same as it was in FC4 but with the addition of MCS. Finally, there is a new policy in FCS called mls; as the name suggests, this includes the MLS system to protect data confidentiality. The domain-type part of the mls policy is based on the strict policy (although not all the daemons from the strict policy are supported - only those from the evaluation list for SPP certification).

It is possible to compile an SELinux policy without support for MLS or MCS features, but so far, no one has chosen to do so. It would save very little memory and would be worth considering only for the smallest embedded machines. It also is possible to use MLS instead of MCS with the targeted policy, but no one has done so, because it would not provide much benefit. System integrity is a precondition for data confidentiality. Therefore, there is no benefit in combining a strong system of confidentiality protection, such as MLS, with anything less than the best protection of system integrity. The strict policy confines all processes and significantly limits most of them. This is the level of integrity protection that is needed to take full advantage of MLS.

In MCS, a process has a range. The high level of the range determines the access granted to files, and the low level determines the default level of files that are created (ranges apply only to processes in MCS).

For an MCS level to dominate another, it must have a set of categories that is a superset of the MCS level that is being dominated. It is possible to have two sensitivity levels for which neither dominates the other (for example, disjoint sets of categories). This is referred to as incomparable levels, and both read and write access will be denied.

To use MCS, first you need to assign sensitivity levels to users. In previous releases of SELinux, it was necessary to edit the policy source and recompile the policy to set the security context that is assigned to users when they log in, which was inconvenient and error-prone. One of the new SELinux features in FCS is the semanage policy management tool. This supports changing the security contexts of users (and adding and removing users) without compiling the policy.

The default configuration of Fedora has the targeted policy that runs all user login sessions in the unconfined_t domain (no access restrictions in the domain-type model), so MCS provides the only SELinux access controls for users. However, a default install of Fedora Core 5 needs to have updates applied before MCS will work correctly. The development of MCS was not complete until after the release of Fedora Core 5.

The first thing you must do when configuring an SELinux system to use MCS is create SELinux identities and login records to map them to UNIX accounts.

Listing 1 is an example of using semanage to add the SELinux identity rjc with a low level of s0:c1 (which means every file the user creates will have category c1 by default) and a high level of SystemHigh, which maps to s0:c0.c1023 (the range of all categories from c0 to c1023 inclusive - the highest level of MCS access) in Fedora Core 6 and to s0:c0.c255 in Fedora Core 5. The -L parameter specifies the default level. When using MCS, you always should make the default level the low end of the range to avoid confusion. The -R option is separate from the range
