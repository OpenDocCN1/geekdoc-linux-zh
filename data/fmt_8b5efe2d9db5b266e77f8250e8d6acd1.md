
Autoresponders automatically generate replies to received messages; they are commonly used to notify others that the recipient is out of the office. Mercifully, Ubuntu does not include one, but you can find and install an autoresponder at Freshmeat.net. If you are subscribed to a mailing list, be aware that automatic responses from your account can be very annoying to others on the list. Please unsubscribe from mail lists before you leave the office with your autoresponder activated.

## Alternatives to Microsoft Exchange Server

One of the last areas in which a Microsoft product has yet to be usurped by open-source software is a replacement for Microsoft Exchange Server. Many businesses use Microsoft Outlook and Microsoft Exchange Server to access email, as well as to provide calendaring, notes, file sharing, and other collaborative functions. General industry complaints about Exchange Server center around scalability, administration (backup and restore in particular), and licensing fees.

A “drop-in” alternative needs to have compatibility with Microsoft Outlook because it’s intended to replace Exchange Server in an environment in which there are Microsoft desktops in existence using Outlook. A “work-alike” alternative provides similar features to Exchange Server, but does not offer compatibility with the Microsoft Outlook client itself; the latter is typical of many of the open-source alternatives.

Several “drop-in” alternatives exist, none of which are fully open source because some type of proprietary connector is needed to provide the services to Microsoft Outlook clients (or provide Exchange services to the Linux Evolution client). For Outlook compatibility, the key seems to be the realization of a full, open implementation of MAPI, the Microsoft Messaging Application Program Interface. That goal is going to be difficult to achieve because MAPI is a poorly documented Microsoft protocol. For Linux-only solutions, the missing ingredient for many alternatives is a usable group calendaring/scheduling system similar in function to that provided by Exchange Server/Outlook.

Of course, independent applications for these functions abound in the open-source world, but one characteristic of “groupware” is its central administration; another is that all components can share information.

The following sections examine several of the available servers, beginning with Microsoft Exchange Server itself and moving toward those applications that have increasing incompatibility with it. None of these servers are provided with Ubuntu.

## Microsoft Exchange Server/Outlook Client

Exchange Server and Outlook seem to be the industry benchmark because of their widespread deployment. They offer a proprietary server providing email, contacts, scheduling, public folders, task lists, journaling, and notes using Microsoft Outlook as the client and MAPI as the API. If you consider what Microsoft Exchange offers as the “full” set of features, no other replacement offers 100% of the features exactly as provided by Microsoft Exchange Server—even those considered “drop-in” replacements. The home page for the Microsoft Exchange server is http://www.microsoft.com/exchange/.

## CommuniGate Pro

CommuniGate Pro is a proprietary, drop-in alternative to Microsoft Exchange Server, providing, email, webmail, LDAP directories, a web server, file server, contacts, calendaring (third party), and a list server. The CommuniGate Pro MAPI Connector provides access to the server from Microsoft Outlook and other MAPI-enabled clients. The home page for this server is http://www.stalker.com/.

## Oracle Collaboration Suite
