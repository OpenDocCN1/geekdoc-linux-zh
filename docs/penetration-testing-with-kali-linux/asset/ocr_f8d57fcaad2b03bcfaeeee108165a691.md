# OffSec

Penetration Testing with Kali Linux

href=http://go.microsoft.com/fflink/?linkid=66138&amp;clcid=0x409

ParsedHtml : 703

Listing 820 - Accessing the SMB share with the silver ticket

Great! We successfully forged a service ticket and got access to the web page as jeffadmin. It's worth noting that we performed this attack without access to the plaintext password or hash of this user.

Once we have access to the password hash of the SPN, a machine account, or user, we can force the related service tickets for any users and permissions. This is a great way of accessing SPNs in later phases of a penetration test, as we need privileged access in most situations to retrieve the password hash of the SPN.

Since silver and golden tickets represent powerful attack techniques, Microsoft created a security patch to update the PAC structure.¹124 With this patch in place, the extended PAC structure field PAC_REQUESTOR needs to be validated by a domain controller. This mitigates the capability to forge tickets for non-domain users if the client and the KDC are in the same domain. Without this patch, we could create silver tickets for domain users that do not exist. The updates from this patch are from October 11, 2022.

In this section, we learned how to force service tickets by using the password hash of a target SPN. SPN in run by a user account in the example, we could do the same for SPNs in the context of a machine account.

# 22.2.5 Domain Controller Synchronization

In production, domains typically rely on more than one domain controller to provide redundancy. The Directory Replication Service (DRS) Remote Protocol¹¹¹²⁵ uses replication¹¹²⁶ to synchronize these redundant domain controllers. A domain controller may request a specific object, like an account, using the IDL_DSGetNCChanges¹¹¹²⁷ API.

Likely for us, the domain controller receiving a request from a known domain controller. not check whether the request has the associated SID has appropriate privileges. If we attempt to issue a rogue request to a domain controller from a user with certain rights it will succeed.

To launch a replication, we need to have the Replicating Directory Changes, Replicating Directory Changes All, and Replicating Directory Changes in Filtered Sets. By default, members of the Domain Admins, Enterprise Admins, and Administrators groups have these rights.

¹¹²⁴ (Microsoft, Support, 2023), https://support.microsoft.com/en-gb/topic/kb-5005830-authentication-updates-cve-2021-42287-9dafac11-e3d0-4c8b-959a-14d3b021041

¹¹²⁵ (Microsoft, 2017), https://msdn.microsoft.com/en-us/library/cc228065.aspx

¹¹²⁶ (Microsoft, 2016), https://technet.microsoft.com/en-us/library/cc77276(v=ws0).aspx

¹¹²⁷ (Microsoft, 2019), https://learn.microsoft.com/en-us/openspec/windows-protocols/ms-drr/b63730ac-641c-431c-9501-28dca6a9184

PWK - © 2023 OffSec Services Limited. All rights reserved.

773