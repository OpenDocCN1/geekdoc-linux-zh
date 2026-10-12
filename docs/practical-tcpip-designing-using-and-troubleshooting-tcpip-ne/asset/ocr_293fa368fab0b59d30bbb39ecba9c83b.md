# ### 8.2 The DNS database is distributed

The DNS is a distributed database. There is no single database or single machine that contains the list of all hosts on the Internet. Instead, when you want to resolve a name, e.g. alice.ibm.com, you query the DNS server at the root of the DNS tree. (There are several of these servers in fact, all containing exactly the same information, and they are called root servers or root name servers.) The root server knows only about its direct children (.com, .edu, .uk, etc.) so it gives you the address of another server – one that knows about the .com domain. Then you query that server, which knows only about its children: it points you to a server that knows about ibm.com. Finally you ask that server for alice’s IP number, and when you receive the answer the process is finished. This happens every time you resolve a name, so you never have to download a HOSTS.TXT file as you did in the old days. Your DNS software retrieves the information automatically, so you always get up-to-date answers, and as soon as I add a machine bob.example.co.uk to my domain, you can resolve it immediately.

That explains how the DNS database is distributed, but it raises another issue: how does a root server know where to find a .com server, and how does a .com server know where the DNS servers for ibm.com are? (What’s to stop a fraudster saying that she runs the servers for ibm.com and redirecting all traffic for IBM to her site?) The DNS uses the concepts of authority and delegation to handle this and to control how the database is distributed in manageable chunks.

# ## Terminology – top-level domains

The children of the root, i.e. the domains .com, .edu, .org, .uk, etc., are called top-level domains (TLDs), as shown in Figure 8.2. Some TLDs (.uk, .ca, .de, .au, …) are country specific: domains within them can be allocated only to organizations in the particular country; they are called country code top-level domains (ccTLDs). The other TLDs (.com, .org, etc.) are called generic top-level domains (gTLDs) because you can obtain a name in these domains irrespective of where you are located (although in practice .gov and .mil are used only for the USA and .edu is only for the USA and Canada).

![](bbox=[0.15, 0.62, 0.92, 0.8])

**Figure 8.2 Top-level domains**

# ## Authority, delegation, and zones

The root server – the server for the root domain – delegates authority for the top-level domains to other organizations. It does this with special entries in the root server database. For example,