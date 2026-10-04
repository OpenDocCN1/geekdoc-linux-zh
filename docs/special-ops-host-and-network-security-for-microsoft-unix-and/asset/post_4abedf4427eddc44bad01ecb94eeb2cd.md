
## Chapter 7 • Securing Exchange and Outlook Web Access

## Figure 7.1 Major Components of Exchange 2000 and Windows 2000 Dependencies

![](img/729efc56f204a2ebffb8295c3a2dfdfb_330_0.png)

The first of these dependencies is the Windows 2000 Active Directory. Previous versions of Exchange included a fairly sophisticated directory service; this directory service was touted by many as the crown jewel of the Exchange platform. This directory contained information about each mailbox server name, message size restrictions and storage restrictions as well as mailbox owner “white pages” information such as address, city and state and telephone number. A sometimes complex process to keep the directories between Exchange 4.0 and 5.x servers had to be maintained. Since Active Directory is capable of providing sophisticated directory services, the need for a separate directory is not necessary, thus Exchange 2000 uses the Windows 2000 Active Directory to store configuration information as well as information about all mailboxes and other mail-enabled objects. The Active Directory bears many references to the earlier versions of the Exchange directory in part to the fact that many of the developers were transferred to the Exchange team. Exchange 2000 servers must maintain communication with at least one Windows 2000 domain controller and global catalog server at all times.

> WARNING
Exchange 2000 will not function if it loses communication with either a domain controller and/or global catalog server. Communications with these servers must be guaranteed in order for message flow to continue.

Prior to Exchange 2000 installation, the Windows 2000 server must have the Internet Information Services (IIS) HTTP, SMTP, and NNTP components installed and running. Once Exchange 2000 is installed, these services do not necessarily need to remain running, but some services (such as Web services or message transport) will not function if they are disabled.

During Exchange 2000 installation, the SMTP and NNTP components are extended to provide additional functionality required by Exchange. Virtual HTTP directories are created to provide access to Outlook Web Access (OWA) supporting folders, mailboxes, and public folders. The Exchange 2000 installation also installs POP3 and IMAP4 services that function as part of.

The IIS SMTP service is extended during the installation of Exchange 2000 to allow the service to expand distribution lists, query the Active Directory for mailbox properties, the routing engine, and provide Exchange-to-Exchange communication. All Exchange 2000–to–Exchange 2000 communication is handled via the SMTP engine; One of the components is called the Advanced Queuing; this component processes every message that is sent on the Exchange server.

## Exchange 2000 Components

Exchange Server is not a single, large program, but rather it is a number of small programs that each carry out specialized services. The Exchange installation process not only install new services, but it extends a number of existing Windows 2000 services. Table 7.1 has a list of the common Exchange 2000 services, that service’s executable service, and the Windows 2000 service on which this service depends.

## Table 7.1 Exchange 2000 Services and Dependencies

| Exchange 2000 Service | Windows 2000 Service Dependencies |
|---|---|
| Microsoft Exchange System Attendant (mad.exe) (Mailer Administrative Daemon, in case you were wondering) | Remote Procedure Call (RPC)<br>Remote Procedure Call (RPC Locator)<br>NT LM Security Support Provider<br>Event Log<br>Workstation |
| Microsoft Exchange Information Store (store.exe) (This service usually consumes most of the RAM in an Exchange server. This is normal.) | IIS Admin Service<br>Microsoft Exchange System Attendant |
| Simple Mail Transport Protocol (SMTP) (process of inetinfo.exe, installed with Windows 2000) | IIS Admin Service |
| Microsoft Exchange Routing Engine (process of inetinfo.exe) | IIS Admin Service |
| Microsoft Exchange IMAP4 (process of inetinfo.exe) | IIS Admin Service<br>Microsoft Exchange Information Store |
| Microsoft Exchange POP3 (process of inetinfo.exe) | IIS Admin Service<br>Microsoft Exchange Information Store |
| Microsoft Exchange MTA (emsta.exe) | IIS Admin Service<br>Microsoft Exchange System Attendant |
| Network Transport Protocol (NNTP) (process of inetinfo.exe, installed with Windows 2000) | IIS Admin Service |
| Microsoft Exchange Search (search.exe) | NT LM Security Support Provider<br>Remote Procedure Call (RPC) |

The first of these dependencies is the Windows 2000 Active Directory. Previous versions of Exchange included a fairly sophisticated directory service; this directory service was touted by many as the crown jewel of the Exchange platform. This directory contained information about each mailbox server name, message size restrictions and storage restrictions as well as mailbox owner “white pages” information such as address, city and state and telephone number. A sometimes complex process to keep the directories between Exchange 4.0 and 5.x servers had to be maintained. Since Active Directory is capable of providing sophisticated directory services, the need for a separate directory is not necessary, thus Exchange 2000 uses the Windows 2000 Active Directory to store configuration information as well as information about all mailboxes and other mail-enabled objects. The Active Directory bears many references to the earlier versions of the Exchange directory in part to the fact that many of the developers were transferred to the Exchange team. Exchange 2000 servers must maintain communication with at least one Windows 2000 domain controller and global catalog server at all times.

> WARNING
Exchange 2000 will not function if it loses communication with either a domain controller and/or global catalog server. Communications with these servers must be guaranteed in order for message flow to continue.

Prior to Exchange 2000 installation, the Windows 2000 server must have the Internet Information Services (IIS) HTTP, SMTP, and NNTP components installed and running. Once Exchange 2000 is installed, these services do not necessarily need to remain running, but some services (such as Web services or message transport) will not function if they are disabled.

During Exchange 2000 installation, the SMTP and NNTP components are extended to provide additional functionality required by Exchange. Virtual HTTP directories are created to provide access to Outlook Web Access (OWA) supporting folders, mailboxes, and public folders. The Exchange 2000 installation also installs POP3 and IMAP4 services that function as part of.

The IIS SMTP service is extended during the installation of Exchange 2000 to allow the service to expand distribution lists, query the Active Directory for mailbox properties, the routing engine, and provide Exchange-to-Exchange communication. All Exchange 2000–to–Exchange 2000 communication is handled via the SMTP engine; One of the components is called the Advanced Queuing; this component processes every message that is sent on the Exchange server.

## Securing Exchange and Outlook Web Access

The first of these dependencies is the Windows 2000 Active Directory. Previous versions of Exchange included a fairly sophisticated directory service; this directory service was touted by many as the crown jewel of the Exchange platform. This directory contained information about each mailbox server name, message size restrictions and storage restrictions as well as mailbox owner “white pages” information such as address, city and state and telephone number. A sometimes complex process to keep the directories between Exchange 4.0 and 5.x servers had to be maintained. Since Active Directory is capable of providing sophisticated directory services, the need for a separate directory is not necessary, thus Exchange 2000 uses the Windows 2000 Active Directory to store configuration information as well as information about all mailboxes and other mail-enabled objects. The Active Directory bears many references to the earlier versions of the Exchange directory in part to the fact that many of the developers were transferred to the Exchange team. Exchange 2000 servers must maintain communication with at least one Windows 2000 domain controller and global catalog server at all times.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_332_0.png)

Prior to Exchange 2000 installation, the Windows 2000 server must have the Internet Information Services (IIS) HTTP, SMTP, and NNTP components installed and running. Once Exchange 2000 is installed, these services do not necessarily need to remain running, but some services (such as Web services or message transport) will not function if they are disabled.

During Exchange 2000 installation, the SMTP and NNTP components are extended to provide additional functionality required by Exchange. Virtual HTTP directories are created to provide access to Outlook Web Access (OWA) supporting folders, mailboxes, and public folders. The Exchange 2000 installation also installs POP3 and IMAP4 services that function as part of.

The IIS SMTP service is extended during the installation of Exchange 2000 to allow the service to expand distribution lists, query the Active Directory for mailbox properties, the routing engine, and provide Exchange-to-Exchange communication. All Exchange 2000–to–Exchange 2000 communication is handled via the SMTP engine; One of the components is called the Advanced Queuing; this component processes every message that is sent on the Exchange server.

During Exchange 2000 installation, the SMTP and NNTP components are extended to provide additional functionality required by Exchange. Virtual HTTP directories are created to provide access to Outlook Web Access (OWA) supporting folders, mailboxes, and public folders. The Exchange 2000 installation also installs POP3 and IMAP4 services that function as part of.

Prior to Exchange 2000 installation, the Windows 2000 server must have the Internet Information Services (IIS) HTTP, SMTP, and NNTP components installed and running. Once Exchange 2000 is installed, these services do not necessarily need to remain running, but some services (such as Web services or message transport) will not function if they are disabled.

During Exchange 2000 installation, the SMTP and NNTP components are extended to provide additional functionality required by Exchange. Virtual HTTP directories are created to provide access to Outlook Web Access (OWA) supporting folders, mailboxes, and public folders. The Exchange 2000 installation also installs POP3 and IMAP4 services that function as part of.

The IIS SMTP service is extended during the installation of Exchange 2000 to allow the service to expand distribution lists, query the Active Directory for mailbox properties, the routing engine, and provide Exchange-to-Exchange communication. All Exchange 2000–to–Exchange 2000 communication is handled via the SMTP engine; One of the components is called the Advanced Queuing; this component processes every message that is sent on the Exchange server.

> WARNING
Exchange 2000 will not function if it loses communication with either a domain controller and/or global catalog server. Communications with these servers must be guaranteed in order for message flow to continue.

Prior to Exchange 2000 installation, the Windows 2000 server must have the Internet Information Services (IIS) HTTP, SMTP, and NNTP components installed and running. Once Exchange 2000 is installed, these services do not necessarily need to remain running, but some services (such as Web services or message transport) will not function if they are disabled.

During Exchange 2000 installation, the SMTP and NNTP components are extended to provide additional functionality required by Exchange. Virtual HTTP directories are created to provide access to Outlook Web Access (OWA) supporting folders, mailboxes, and public folders. The Exchange 2000 installation also installs POP3 and IMAP4 services that function as part of.

The IIS SMTP service is extended during the installation of Exchange 2000 to allow the service to expand distribution lists, query the Active Directory for mailbox properties, the routing engine, and provide Exchange-to-Exchange communication. All Exchange 2000–to–Exchange 2000 communication is handled via the SMTP engine; One of the components is called the Advanced Queuing; this component processes every message that is sent on the Exchange server.

> WARNING
Exchange 2000 will not function if it loses communication with either a domain controller and/or global catalog server. Communications with these servers must be guaranteed in order for message flow to continue.

Prior to Exchange 2000 installation, the Windows 2000 server must have the Internet Information Services (IIS) HTTP, SMTP, and NNTP components installed and running. Once Exchange 2000 is installed, these services do not necessarily need to remain running, but some services (such as Web services or message transport) will not function if they are disabled.

During Exchange 2000 installation, the SMTP and NNTP components are extended to provide additional functionality required by Exchange. Virtual HTTP directories are created to provide access to Outlook Web Access (OWA) supporting folders, mailboxes, and public folders. The Exchange 2000 installation also installs POP3 and IMAP4 services that function as part of.

The IIS SMTP service is extended during the installation of Exchange 2000 to allow the service to expand distribution lists, query the Active Directory for mailbox properties, the routing engine, and provide Exchange-to-Exchange communication. All Exchange 2000–to–Exchange 2000 communication is handled via the SMTP engine; One of the components is called the Advanced Queuing; this component processes every message that is sent on the Exchange server.

> WARNING
Exchange 2000 will not function if it loses communication with either a domain controller and/or global catalog server. Communications with these servers must be guaranteed in order for message flow to continue.

Prior to Exchange 2000 installation, the Windows 2000 server must have the Internet Information Services (IIS) HTTP, SMTP, and NNTP components installed and running. Once Exchange 2000 is installed, these services do not necessarily need to remain running, but some services (such as Web services or message transport) will not function if they are disabled.

> WARNING
Exchange 2000 will not function if it loses communication with either a domain controller and/or global catalog server. Communications with these servers must be guaranteed in order for message flow to continue.

## Understanding the Security Risks Associated with Exchange 2000

In order to successfully harden Exchange 2000 servers against attacks on the server, it is important that you understand the potential security risks that the Exchange server may face. This includes vulnerabilities that may be exploited by an unscrupulous administrator, a member of your user community, or an external hacker. This includes threats to information that may be discerned through Active Directory, someone accessing critical database or log files, network sniffing, forgeries, or malicious code installed on the Exchange 2000 server. This section of this chapter covers some of the vulnerabilities that may be found in Exchange 2000; the following section addresses how to make sure these and other weaknesses are fixed.
