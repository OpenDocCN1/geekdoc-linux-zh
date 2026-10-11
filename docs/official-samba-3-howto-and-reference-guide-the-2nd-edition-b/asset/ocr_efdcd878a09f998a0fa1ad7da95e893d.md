# Figure 4.1 An Example Domain.

![](bbox=[0.1, 0.1, 0.9, 0.45])

Where is the right place to make mistakes? Only out of harms way. If you are going to make mistakes, then please do it on a test network, away from users, and in such a way as to not inflict pain on others. Do your learning on a test network.

# 4.1 Features and Benefits

> *What is the key benefit of Microsoft Domain Security?*

In a word, *single sign-on*, or SSO for short. To many, this is the Holy Grail of MS Windows NT and beyond networking. SSO allows users in a well-designed network to log onto any workstation that is a member of the domain that contains their user account (or in a domain that has an appropriate trust relationship with the domain they are visiting) and they will be able to log onto the network and access resources (shares, files, and printers) as if they are sitting at their home (personal) workstation. This is a feature of the domain security protocols.

The benefits of domain security are available to those sites that deploy a Samba PDC. A domain provides a unique network security identifier (SID). Domain user and group security identifiers are comprised of the network SID plus a relative identifier (RID) that is unique to the account. User and group SIDs (the network SID plus the RID) can be used to create access control lists (ACLs) attached to network resources to provide organizational access control. UNIX systems recognize only local security identifiers.