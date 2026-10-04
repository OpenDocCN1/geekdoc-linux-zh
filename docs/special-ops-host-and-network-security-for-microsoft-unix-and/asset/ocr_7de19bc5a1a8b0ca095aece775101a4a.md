# Chapter 6 • Securing Active Directory

# Figure 6.11 Taking Ownership of the Object

![](bbox=[0.313, 0.11, 0.642, 0.344])

After the ownership is transferred, the object is in full control of the new user and not the administrator. In order to make changes to the object, an administrator will have to take ownership back.

# Privilege Escalation

In a Windows environment, each subject (user, computer, and so on) that wants to do something with another object/file/process, has to obtain an authorization from the Access Control List that is associated with the object. ACLs use so-called Security Identifiers (SIDs) to uniquely identify these subjects. When a subject (usually called a *principal*) is authenticated, the result of the process is the set of SIDs containing the SID of the principal itself and for all groups he is a member of. When the principal requests access to a resource, all of the SIDs are checked against the resource's ACL to verify that he is authorized to do what she wants.

When a domain trusts another domain, this also means that it trusts the second domain SIDs. The first domain considers all SIDs for a principal from another domain correct and reliable. Combined, with a feature called SIDHistory, this could to an interesting attack.

SIDHistory was introduced in Windows 2000 as a tool to help in migration of users between domains without having to re-establish all of their permissions. The primary identifier of a user is not his name, but his SID. If you delete and re-create a user with the same name, it will be considered as a completely different one. On the other hand, the renaming of a user does not affect anything, because his SID remains unchanged.