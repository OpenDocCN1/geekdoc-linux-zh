# 22 Attacking Active Directory Authentication

In this Module, we will cover the following Learning Units:

+   - Understanding Active Directory Authentication
- Performing Attacks on Active Directory Authentication

Having enumerated user accounts, group memberships, and registered Service Principal Names in the previous Module Active Directory Introduction and Enumeration, let's attempt to use this information to compromise Active Directory.

In this Module, we will first explore authentication mechanisms of Active Directory (AD) and learn how Windows caches objects as password hashes and tickets. Next, we will get familiar with the attack methods targeting these authentication mechanisms during different phases of a penetration test to obtain user credentials and access to systems and services. For the purpose of this Module, we will target the sample domain (corp.com) as in the previous Module.

# 22.1 Understanding Active Directory Authentication

This Learning Unit covers the following Learning Objectives:

+   - Understand NTLM Authentication
- Understand Kerberos Authentication
- Become familiar with cached AD credentials

Active Directory supports multiple authentication protocols that implement authentication to Windows computers as well as running Linux and macOS.

> Active Directory supports several older protocols including WDigest While these may be useful for older operating systems like Windows 7 or Windows Server 2008 R2, we will only focus on more modern authentication protocols in this Learning Unit.

In this Learning Unit, we will discuss the details of NTLM and Kerberos authentication. In addition, we will explore where and how AD credentials are cached on Windows systems.

# 22.1.1 NTLM Authentication

In Password Attacks, we briefly discuss what NTLM is and where to find its hashes. In this section, we'll explore NTLM authentication in the context of Active Directory.