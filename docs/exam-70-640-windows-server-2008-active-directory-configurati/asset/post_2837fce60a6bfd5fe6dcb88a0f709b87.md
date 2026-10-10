
## Lesson 3: Managing Replication
- Managing Replication
- Triggering Manual Replication
- Monitoring Replication
- Summary Skill Matrix
- Knowledge Assessment
- Case Scenarios

## Lesson 4: Global Catalog and Flexible Single Master Operations (FSMO) Roles
- Objective Domain Matrix
- Key Terms
- Understanding the Global Catalog
- Understanding the Functions of the Global Catalog
- Configuring Additional Global Catalog Servers
- Understanding Flexible Single Master Operations (FSMO) Roles
- Placing FSMO Role Holders
- Managing FSMO Roles
- Viewing the FSMO Role Holders
- Transferring a FSMO Role Holder
- Seizing a FSMO Role
- Summary Skill Matrix
- Knowledge Assessment
- Case Scenarios
- Workplace Ready

## Lesson 5: Active Directory Administration
- Objective Domain Matrix
- Key Terms
- Understanding User Accounts
- Understanding Group Accounts
- Working with Default Groups
- Understanding Special Identity Groups and Local Groups
- Developing a Group Implementation Plan
- Creating Users, Computers, and Groups
- Using Batch Files
- Using CSVDE
- Using LDIFDE
- Using Windows Scripting Host
- Summary Skill Matrix
- Knowledge Assessment
- Case Scenarios

## Lesson 6: Security Planning and Administrative Delegation
- Objective Domain Matrix
- Key Terms
- Planning and Implementing Account Security
- Using Passwords
- Educating Users on the Importance of Passwords
- Configuring Strong Passwords
- Securing Administrative Access to Active Directory
- Planning an Organizational Unit Strategy
- Creating an OU Structure
- Using OUs to Delegate Active Directory Management Tasks
- Moving Objects Between OUs
- Summary Skill Matrix
- Knowledge Assessment
- Case Scenarios

## Lesson 7: Introduction to Group Policy
- Objective Domain Matrix
- Key Terms
- Introducing Group Policy
- Understanding the Benefits of Group Policy
- Defining Group Policy Architecture
- Viewing the Group Policy Container
- Viewing Group Policy Templates
- Using the Group Policy Management Console
- Configuring Group Policy Settings
- Understanding Group Policy Processing
- Configuring Exceptions to GPO Processing
- Summary Skill Matrix
- Knowledge Assessment
- Case Scenarios

## Lesson 8: Configuring the User and Computer Environment Using Group Policy
- Objective Domain Matrix
- Key Terms
- Configuring Security Policies Using Group Policy Objects
- Configuring Account Policies
- Configuring Fine-Grained Password Policies
- Configuring the Kerberos Policy
- Defining Local Policies
- Planning and Configuring an Audit Policy
- Customizing Event Log Policies
- Understanding Restricted Groups
- Customizing System Services, Registry, and File System Settings
- Configuring Folder Redirection
- Configuring Offline Files
- Using Disk Quotas
- Maintaining and Optimizing Group Policy
- Manually Refreshing Group Policy
- Optimizing Group Policy Processing
- Summary Skill Matrix
- Knowledge Assessment
- Case Scenarios
- Filtering Group Policy Scope
- Configuring Security Group Filtering
- Configuring WMI Filtering
- Determining and Troubleshooting Effective Policy Settings
- Using the Resultant Set of Policy Wizard
- Creating a Group Policy Modeling Query
- Creating a Group Policy Results Query
- Using GPRESULT
- Summary Skill Matrix
- Knowledge Assessment
- Case Scenarios

## Lesson 9: Performing Software Installation with Group Policy
- Objective Domain Matrix
- Key Terms
- Managing Software through Group Policy
- Repackaging Software
- Implementing Software Using Group Policy
- Assigning an Application to a User or Computer
- Publishing an Application
- Customizing Software Installation Packages
- Using Software Categories
- Configuring Software Restriction Policies
- Configuring Software Restriction Rules
- Summary Skill Matrix
- Knowledge Assessment
- Case Scenarios

## Lesson 10: Planning a Group Policy Management and Implementation Strategy
- Objective Domain Matrix
- Key Terms
- Managing Group Policy
- Introducing the Group Policy Management MMC Snap-In
- Managing an Individual GPO
- Configuring Starter GPOs

## Lesson 11: Active Directory Maintenance, Troubleshooting, and Disaster Recovery
- Objective Domain Matrix
- Key Terms
- Maintaining Active Directory
- Backing Up Active Directory
- Restoring Active Directory
- Restoring Active Directory Using Normal Replication
- Restoring Active Directory Using WBADMIN and NTDSUTIL
- Performing an Authoritative Restore
- Monitoring Active Directory
- Understanding Event Logs
- Using the Reliability and Performance Monitor
- Diagnosing and Troubleshooting Active Directory
- Summary Skill Matrix
- Knowledge Assessment
- Case Scenarios

## Lesson 12: Configuring Name Resolution and Additional Services
- Objective Domain Matrix
- Key Terms
- DNS Name Resolution
- Understanding Name Resolution
- Introducing the Domain Name System (DNS)
- Understanding Domain Hierarchy Levels
- Understanding DNS Referrals and Queries
- Understanding Reverse Name Resolution
- Combining Internal and External DNS Name Resolution
- Understanding DNS Server Types
- Creating DNS Zones
- Configuring a Standard DNS Zone
- Configuring Zone Transfers
- Configuring Active Directory-Integrated Zones
- Configuring Custom Application Directory Partitions
- Configuring DNS Client Settings and DHCP/WINS Integration
- Configuring Additional Services
- Summary Skill Matrix
- Knowledge Assessment
- Case Scenarios

## Lesson 13: Configuring Active Directory Certificate Services
- Objective Domain Matrix
- Key Terms
- Introducing Active Directory Certificate Services
- Introducing the Public Key Infrastructure
- Installing Active Directory Certificate Services
- Configuring Certificate Revocation
- Configuring Certificate Templates
- Managing Certificate Enrollments
- Configuring Certificate Auto-Enrollment for Wireless Networks
- Configuring CA Server Settings
- Configuring Key Archival and Recovery
- Maintaining a Windows Server 2008 CA
- Summary Skill Matrix
- Knowledge Assessment
- Case Scenarios

Appendix A
Appendix B
Glossary
Index

## Overview of Active Directory Domain Services

### LESSON 1

| KEY TERMS | |
| :--- | :--- |
| Active Directory Domain Services (AD DS) | external trust |
| application partition | fault tolerant |
| attribute | forest |
| Configuration NC | forest root domain |
| container object | functional levels |
| cross-forest trust | globally unique identifier (GUID) |
| delegation | inbound replication |
| directory service | IP address |
| distinguished name (DN) | Knowledge Consistency Checker (KCC) |
| domain | leaf object |
| domain controller (DC) | Lightweight Directory Access Protocol (LDAP) |
| Domain Name System (DNS) | link-value replication |
| Domain NC | locator service |
| domain tree | loose consistency |
| | naming context (NC) |
| | object |
| | organizational unit (OU) |
| | outbound replication |
| | partition |
| | publishing |
| | Read-Only Domain Controller (RODC) |
| | replication |
| | rolling upgrades |
| | schema |
| | Schema NC |
| | shortcut trust |
| | site |
| | SRV record |
| | trust relationship |

Lucerne Publishing is a publisher of medical textbooks that maintains offices in London, Tokyo, New York, and Bangalore. In the past, the Lucerne Publishing staff has used multiple usernames and passwords to access a small number of file servers and applications, but the company has grown significantly in recent years and this growth has made managing this process unwieldy. Lucerne has decided to deploy Windows Server 2008 to provide centralized authentication and authorization of users across its worldwide locations to provide users with a single username and password that will provide access to resources across the enterprise.

After completing this lesson, you will be able to describe the Active Directory Domain Services role in Windows Server 2008 and its functions and benefits. You will also develop an understanding of the components of an Active Directory environment, including forests, sites, domains, domain trees, and organizational units (OUs). We will discuss how to design the physical and logical structure of an Active Directory network and delve into Active Directory’s naming standards and their importance to a well-functioning Active Directory environment. Finally, you will understand and assess Active Directory domain and functional levels based on the needs of an organization’s network environment as well as the trust models used by Active Directory and the role that Active Directory trusts play in resource accessibility across multiple organizations.
