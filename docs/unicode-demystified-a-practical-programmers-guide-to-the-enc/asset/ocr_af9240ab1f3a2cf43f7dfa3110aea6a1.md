• AERO Air-transport industry
• BIZ Business
• COOP Cooperatives
• INFO Unrestricted use
• MUSEUM Museums
• NAME Name registries

With Internet addresses, domain names used to be assigned by the Network Information Center (NIC [page 362]). Now they are assigned by several companies. A system's full name, referred to as its fully qualified domain name (FQDN), is unambiguous in the way that a simple hostname cannot be. The system oekffe.berkeley.edu at the University of California, Berkeley (Figure 9-3) is not the same as one named oekffe.moma.org, which might represent a host at the Museum of Modern Art. The domain name not only tells you something about where the system is located but also adds diversity to the name space to avoid confusion when different sites choose similar names for the them.

Unlike the filesystem hierarchy, the top-level domain name in the United States appears last (reading from left to right). Also, domain names are not case sensitive. The names oekffe.berkeley.edu, oekffe.Berkeley.edu, and oekffe.Berkeley.EDU refer to the same computer. Once a domain has been assigned, the local site is free to extend the hierarchy to meet local needs.

With DNS, mail addressed to user@tcorp.com can be delivered to the tcorp.com computer that handles the corporate mail and knows how to forward messages to user mailboxes on individual machines. As the company grows, the site administrator might decide to create organizational or geographical subdomains. The name tcorp.ca.tcorp.com might refer to a system that supports California offices, with alpha.co.tcorp com dedicated to Colorado. Functional subdomains might be another choice, with tcorp.sales.tcorp.com and alpha.dev.tcorp.com representing the sales and development divisions, respectively.

![](bbox=[0.19955, 0.71335, 0.8824500000000001, 0.8765])