```
# s0:c8=CompanyConfidential
# s0:c1=PatientRecord
# s0:c2=Unclassified
# s0:c3=TopSecret
# s0:tc1,c3=CompanyConfidentialRedHat
s0=:
s0-s0:c0,c255=SystemLow-SystemHigh
s0:c0=SystemHigh
```

And, the following is an example of how to use semanage to change the human-readable translations of MCS labels in Fedora Core 6:

```
# semanage translation -a -T ProjectA s0:c8
# semanage translation -l
```

| Level          | Translation              |
|----------------|--------------------------|
| s0             |                          |
| s0-s0:c0.c1023 | SystemLow-SystemHigh     |
| s0:c0          | ProjectA                 |
| s0:c0.c1023    | SystemHigh               |

Figure 1 shows the access that processes are granted to files for all combinations of the categories HR and financial.

MCS is designed with ease of use as a major concern. At the current time, its design is to control only file access. It also controls privacy (the system interface for strong, Tracer and debuggers) to prevent an unprivileged process from using a debugger to capture secret data from a more-privileged process.

The fact that MCS controls only file access does permit information leaks through filenames, and cooperating processes may use TCP, UDP, UNIX domain sockets or named pipes to transfer data. It was designed this way intentionally, because restricting all forms of inter-process communication will break many programs and make the entire system more difficult to use. The MLS policy (which is available in Fedora Core 5 and above but not enabled by default) restricts such communication methods, which is one of the reasons why it is regarded as being too difficult for most people to use.

When designing MCS, we decided not to try to prevent two cooperating users from inappropriately sharing data. We also decided not to prevent a user from reading a file with secret data and then writing that data to a file with a less secret label. Again, the MLS policy restricts these operations, but it is too difficult for most people to use.

![](bbox=[0.07, 0.73, 0.49, 0.95])

MCS and MLS are designed to protect confidentiality of data; they rely on the domain-type model to protect system integrity. FCS comes with three policies. The default is targeted, which offers much the same integrity protections as is did in FC4 but has the addition of MCS to protect data confidentiality. The next option is the strict policy, which, again, is much the same as it was in FC4 but with the addition of MCS. Finally, there is a new policy in FCS called mls; as the name suggests, this includes the MLS system to protect data confidentiality. The domain-type part of the mls policy is based on the strict policy (although not all the daemons from the strict policy are supported-only those from the evaluation list for SPP certification).

It is possible to compile an SELinux policy without support for MLS or MCS features, but so far, no one has chosen to do so. It would save very little memory and would be worth considering only for the smallest embedded machines. It also is possible to use MLS instead of MCS with the targeted policy, but no one has done so, because it would not provide much benefit. System integrity is a precondition for data confidentiality. Therefore, there is no benefit in combining a strong system of confidentiality protection, such as MLS, with anything less than the best protection of system integrity. The strict policy confines all processes and significantly limits most of them. This is the level of integrity protection that is needed to take full advantage of MLS.

In MCS, a process has a range. The high level of the range determines the access granted to files, and the low level determines the default level of files that are created (ranges apply only to processes in MCS).

For an MCS level to dominate another, it must have a set of categories that is a superset of the MCS level that is being dominated. It is possible to have two sensitivity levels for which neither dominates the other (for example, disjoint sets of categories). This is referred to as incomparable levels, and both read and write access will be denied.

To use MCS, first you need to assign sensitivity levels to users. In previous releases of SELinux, it was necessary to edit the policy source and recompile the policy to set the security context that is assigned to users when they log in, which was inconvenient and error-prone. One of the new SELinux features in FCS is the semanage policy management tool. This supports changing the security contexts of users (and adding and removing users) without compiling the policy.

The default configuration of Fedora has the targeted policy that runs all user login sessions in the unconfined_t domain (no access restrictions in the domain-type model), so MCS provides the only SELinux access controls for users. However, a default install of Fedora Core 5 needs to have updates applied before MCS will work correctly. The development of MCS was not complete until after the release of Fedora Core 5.

The first thing you must do when configuring an SELinux system to use MCS is create SELinux identities and login records to map them to UNIX accounts.

Listing 1 is an example of using semanage to add the SELinux identity rjc with a low level of s0:c1 (which means every file the user creates will have category c1 by default) and a high level of SystemHigh, which maps to s0:c0.c1023 (the range of all categories from c0 to c1023 inclusive-the highest level of MCS access) in Fedora Core 6 and to s0:c0.c255 in Fedora Core 5. The -L parameter specifies the default level. When using MCS, you always should make the default level the low end of the range to avoid confusion. The -R option is separate from the range