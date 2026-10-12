to be especially good for articles describing concepts and for answering broader questions like “why would I want to do X?” or “how would I configure my network to do Y?”

Windows-2000, much more than NT 4.0, is an architecture truly designed for the Internet. CIFS (Common Internet File System) is Microsoft's Windows Networking for the Internet. It hasn't been adopted as an IETF Internet standard and discussion on the net seems to have languished for a couple of years, but this appears to be the future direction for Microsoft file- and print-sharing systems, and getting full documentation of how it works remains a problem. See:

+   - http://www.theregister.co.uk/content/53/24490.html Why Microsoft's EU 'concession' is no concession at all

“Peer-to-peer networking” is increasingly being used on the Internet, as a way to avoid overloading of popular servers in the usual client/server model of interaction. It refers to end-user machines interacting directly with one another rather than acting as clients to dedicated servers – Napster is (or was?) an example, as are Gnutella and KaZaA. Both on the Internet and in Windows Networking the key idea is that client machines can automatically discover and use resources instead of being pre-configured to use specific servers. For more information:

+   - http://www.peer-to-peer.org
+   - http://www.computer.org/internet/v6n1/ Jan/Feb-2002 IEEE Internet Computing Peer-to-Peer Networks in Action

# NetBIOS and NetBEUI

We only mentioned NetBEUI to suggest you don't use it unless you have a good reason to. Nowadays almost nobody needs it, so if you don't know whether you need it or not, the chances are you don't. (You can always disable it for a couple of weeks on your own machine and see if anything breaks. And even if NetBEUI is being used, it can easily be that NetBIOS over TCP/IP could perform the same functions for you.) A common source of confusion is that NetBEUI stands for NetBIOS Extended User Interface. Ignore that – on NT, NetBEUI and NetBIOS are completely separate and different things.

If you run NetBEUI on your systems it can provide a “back door” around any TCP/IP-based security systems you have in place (Module 24.8). It can also cause name resolution problems (see Chapter 19, Notes). Ideally use only a single protocol, i.e. TCP, and not IPX and not NetBEUI.

For a comparison of TCP/IP, IPX/SPX and NetBEUI see:

+   - MS-KB-Q128233 Comparison of Windows NT Network Protocols

The NetBIOS Interface NT Service is not the whole NetBIOS networking subsystem – only a very small part of it. It's a specific service that lets you configure very low-level details of the bindings of protocols to network adapters, which typically you have to do only for non-Microsoft applications, such as Lotus Notes. Most Microsoft applications don't require it although it's impossible to get a definitive list of which ones do use it (and if you disable it and try to use RAS for dial-up networking, you'll get an Error 720). For secure installations many people do disable it.