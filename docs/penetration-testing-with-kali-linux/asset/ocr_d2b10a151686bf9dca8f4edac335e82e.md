# OffSec

Penetration Testing with Kali Linux

+   * Find Workstations where Domain Users can RDP
* Find Servers where Domain Users can RDP
* Find Computers where Domain Users are Local Admin
* Shortest Path to Domain Admins from Owned Principals

Unfortunately, none of these queries return any results. This means BloodHound didn't identify any workstations or servers where Domain Users can log via RDP.

In addition, no Domain Users are a local Administrator on any computer objects. Therefore, we don't have privileged access on any domain computers as john or marcus.

Finally, there are no direct paths from owned users to the Domain Admins group that BloodHound could identify.

These pre-built queries are often a quick and powerful way to identify low hanging fruit in our quest to elevate our privileges and gain access to other systems. Because BloodHound didn't provide us with actionable vectors, we need to revert to other methods.

> We could also use PowerView or LDAP queries to obtain all of this information. However, in most penetration tests, we want to use BloodHound first as out of the other methods that can be quite overwhelming. It's an effective and powerful tool to gain a deeper understanding of the Active Directory environment in a short amount of time. We can also use raw or pre-built queries to identify highly complex attack vectors and display them in an interactive graphical view.

We further enumerate the domain in the next section, let's summarize the information we've obtained so far. We identified four computer objects and four user accounts and learned that becy is a member of the Domain Admins group, making it a high value target. Furthermore, we ruled out some vectors that would have provided us access to other systems or privileged users.

# 24.4.2 Services and Sessions

In the previous section, we performed basic enumeration to obtain an understanding of the Active Directory environment.

In this section, we'll further enumerate the target network to identify potential attack vectors. First, we'll review all active user sessions on machines. Then, we'll examine user accounts for the existence of SPNs.¹¹¹⁹⁹ Finally, we'll leverage tools such as Nmap and CrackMapExec via SOCS¹¹²⁰⁰ proxy to identify accessible services.

1199 (Microsoft Learn, 2021), https://learn.microsoft.com/en-us/windows/win32/ad/service-principal-names

1200 (Wikipedia, 2022), https://en.wikipedia.org/wiki/SOCKS

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

841