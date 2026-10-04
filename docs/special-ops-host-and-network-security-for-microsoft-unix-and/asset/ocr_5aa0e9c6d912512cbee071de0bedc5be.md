# Chapter 7 • Securing Exchange and Outlook Web Access

# Table 7.1 Exchange 2000 Services and Dependencies

| Exchange 2000 Service | Windows 2000 Service Dependencies |
|---|---|
| Microsoft Exchange System Attendant (mad.exe) (Mailer Administrative Daemon, in case you were wondering) | Remote Procedure Call (RPC)<br>Remote Procedure Call (RPC Locator)<br>NT LM Security Support Provider<br>Event Log<br>Workstation |
| Microsoft Exchange Information Store (store.exe) (This service usually consumes most of the RAM in an Exchange server. This is normal.) | IIS Admin Service<br>Microsoft Exchange System Attendant |
| Simple Mail Transport Protocol (SMTP) (process of inetinfo.exe, installed with Windows 2000) | IIS Admin Service |
| Microsoft Exchange Routing Engine (process of inetinfo.exe) | IIS Admin Service |
| Microsoft Exchange IMAP4 (process of inetinfo.exe) | IIS Admin Service<br>Microsoft Exchange Information Store |
| Microsoft Exchange POP3 (process of inetinfo.exe) | IIS Admin Service<br>Microsoft Exchange Information Store |
| Microsoft Exchange MTA Stacks (emsmta.exe) | IIS Admin Service<br>Microsoft Exchange System Attendant |
| Network New Transport Protocol (NNTP) (process of inetinfo.exe, installed with Windows 2000) | IIS Admin Service |
| Microsoft Exchange Search (msearch.exe) | NT LM Security Support Provider<br>Remote Procedure Call (RPC) |

The first Exchange 2000-specific component that is the Microsoft Exchange system attendant. The system attendant service runs a number of different processes. One of these is the DSA cache; this cache keeps information that has been recently queried from Active Directory. The default cache lifetime is five minutes. As a general rule, components such as the information store and IIS use the DSA cache rather than querying Directory over and again; the exception to this is the SMTP Advanced Queuing Engine

![](bbox=[0.068, 0.943, 0.292, 0.97])