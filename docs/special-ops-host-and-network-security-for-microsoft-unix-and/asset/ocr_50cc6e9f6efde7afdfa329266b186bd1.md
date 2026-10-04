# Chapter 14 • Attacking and Defending Unix

often the case that there is an information breakdown that ultimately results in the poor design of a system. In this scenario, two distinct situations emerge:

+   - Insufficient information

+   - Irrelevant information

# Gathering Sufficient Information

One breakdown in information gathering is the gathering of an insufficient quantity of information. This error is common because information gathering can be extremely complex. Gathering information to create a secure system design must go beyond only taking into account the purpose of the system. A system that will act as an e-mail server or SQL database server is affected by a number of variables in the network environment.

Considerations such as management and network design must also be taken into account when planning a system. For example, a host that is destined to sit on a public network is subject to stricter access control requirements than that one will act as a file server on a private network. This is further complicated by such factors as the method of management, software used to monitor hosts, and what kind of access users will need to the host.

Before information gathering can occur, you must decide how much information is needed, and what information is needed. Figure 14.4 shows a short checklist of basic information required. This list can be expanded or contracted to fit your needs. A list of information need not be a formal document, though it should be as legible as possible. This document should be retained in the maintenance logbook kept for the system, and should be legible and detailed enough to give future administrators an idea as to why design decisions were made, and what influences were taken into account when the initial model was developed. As you will see, information is a double-edged sword that can add unneeded complexity.

# Figure 14.4 Checklist of Information to Gather when Planning a Secure Server

| Purpose Of Server | Mail Server |
|---|---|
| Operating System | Solaris |
| Neighbor Servers | Gateway01, www |
| Required Software | Postfix, Apache, Imp |
| | Continued |

![](bbox=[0.068, 0.946, 0.296, 0.973])