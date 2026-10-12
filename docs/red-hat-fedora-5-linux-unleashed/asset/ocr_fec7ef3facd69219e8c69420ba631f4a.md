**NOTE**

Autoreponders automatically generate replies to received messages; they are commonly used to notify others that the recipient is out of the office. Mercurially, Fedora does not include one, but you can find and install an autoresponder at Fresmnet.net. If you subscribe to a mailing list, be aware that automatic responses from your account can be very annoying to others on the list. Please unsubscribe from mail lists before you leave the office with your autoresponder activated.

# Alternatives to Microsoft Exchange Server

One of the last areas in which a Microsoft product has yet to be usurped by open source software is a replacement for MS Exchange Server. Many businesses use MS Outlook and MS Exchange Server to access email, as well as to provide calendaring, notes, file sharing, and other collaborative functions. General industry complaints about Exchange Server center around scalability, administration (backup and restore in particular), and licensing fees.

A drop-in alternative needs to have compatibility with MS Outlook because it’s intended to replace Exchange Server in an environment in which there are Microsoft desktops in existence using Outlook. A work-alike alternative provides similar features to Exchange Server, but does not offer compatibility with the MS Outlook client itself; the latter is typical of many of the open source alternatives.

There are several drop-in alternatives, none of which is fully open source because some type of proprietary connector is needed to provide the services to MS Outlook clients (or provide Exchange services to the Linux Evolution client). For Outlook compatibility, the key seems to be the realization of a full, open implementation of MAPI, Microsoft’s Messaging Application Program Interface. That goal is going to be difficult to achieve because MAPI is a poorly documented Microsoft protocol. For Linux-only solutions, the missing ingredient for many alternatives is a usable group calendaring/scheduling system similar in function to that provided by Exchange Server/Outlook.

Of course, independent applications for these functions abound in the open source world, but one characteristic of groupware is its central administration; another is that all components can share information.

The following sections examine several of the available servers, beginning with MS Exchange Server itself and moving toward those applications that have increasing incompatibility with it. None of these servers are provided with Fedora.

# Microsoft Exchange Server/Outlook Client

Exchange Server and Outlook seem to be the industry benchmark because of their wide-spread deployment. They offer a proprietary server providing email, contacts, scheduling, public folders, task lists, journaling, and notes using MS Outlook as the client and MAPI as the API. If you consider what MS Exchange offers as the full set of features, no other