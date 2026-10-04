# Chapter 7 • Securing Exchange and Outlook Web Access

As and Send As permissions. These permissions inherit from the organization or administrative group object all the way down to mailbox. It is a very good practice to regularly confirm that these permissions have not been accidentally assigned or that the default permissions have not been removed. Check at both the Exchange organization object level as well as the administrative group.

# Figure 7.11 Security at the Exchange Organization Level

![](bbox=[0.318, 0.227, 0.638, 0.483])

> Don't you see the Security property page in Exchange System Manager? It is intentionally hidden and must be enabled using a Registry key. Open the HKEY_CURRENT_USER user tree of the Registry and navigate to \Software\Microsoft\Exchange\EXAdmin. Create a value called ShowSecurityTabPage of type REG_DWORD and set the data to 0x1. Next time you load Exchange System Manager, the Security property page will be available on the Organization and Administrative Group containers.

# Enabling SSL for Internet or Remote Clients

If you have remote clients using Outlook Web Access (OWA) or that are POP3, IMAP4, NNTP clients, you must implement SSL. As I demonstrated earlier in this chapter, intercepting e-mail data and passwords is trivial provided you can a network analyzer in the path of the IP diagrams traveling between the client and the Exchange server.