# ## 21. Active Directory Attacks

Microsoft Active Directory Domain Services,600 often referred to as Active Directory (AD), is a service that allows system administrators to update and manage operating systems, applications, users, and data access on a large scale. Since Active Directory can be a highly complex and granular management layer, it poses a very large attack surface and warrants attention.

In this module, we will introduce Active Directory and demonstrate enumeration, authentication, and lateral movement techniques.

# ### 21.1 Active Directory Theory

Let's begin with a brief overview of basic Active Directory concepts and terms to lay down a foundation before we move into enumeration and exploitation.

Active Directory consists of several components. The most important component is the domain controller (DC),601 which is a Windows 2000-R2 server with the Active Directory Domain Services role installed. The domain controller is the hub and core of Active Directory because it stores all information about how the specific instance of Active Directory is configured. It also enforces a vast variety of rules that govern how objects within a given Windows domain interact with each other, and what services and tools are available to end users. The power and complexity of Active Directory is founded on incredible granularity of controls available to network administrators.

> "There are three different versions of Windows server operating systems. The first was the original “desktop experience” version. Server Core,602 introduced with Windows Server 2008 R2, is a minimal server installation without a dedicated graphical interface. Server Nano,603 the most recent version, was introduced in Windows Server 2016 and is even more minimal than Server Core. The standard “desktop experience” and Server Core editions can function as domain controllers. The Nano edition can not."

When an instance of Active Directory is configured, a domain is created with a name such as corp.com where corp is the name of the organization. Within this domain, we can add various types of objects, including computer and user objects.

System administrators can (and almost always do) organize these objects with the help of Organizational Units (OU). 604 OUs are comparable to file system folders in that they are containers used to store and group other objects. Computer objects represent actual servers and workstations

600 (Microsoft, 2017). https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/virtual-do/active-directory-domain-services-overview  
601 (Microsoft, 2014). https://technet.microsoft.com/library/cc784338(v=ws.10).aspx  
602 (Microsoft, 2008). https://msdn.microsoft.com/en-us/library/ee391626(v=vs.85).aspx  
603 (Microsoft, 2017). https://docs.microsoft.com/en-us/windows-server/get-started/getting-started-with-nano-server  
604 (Microsoft, 2018). https://technet.microsoft.com/en-us/library/cc978003.aspx