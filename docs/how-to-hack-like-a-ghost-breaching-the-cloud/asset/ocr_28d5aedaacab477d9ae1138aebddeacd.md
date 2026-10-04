![](bbox=[0.25, 0.07, 0.75, 0.23])

Figure 4-6: Link to an MXR Ad survey found in the logfile snippet

This must be one of these surveys MXR Ads uses to gather seemingly harmless information about people. Attempting to pwn MXR Ads or Gretsch Politico through one of their pernicious forms is quite tempting, but we are still in the midst of our reconnaissance work, so let’s just note this for a later attempt.

# Pulling Web Domains

Passive reconnaissance has not yielded us many entry points so far. I believe it’s time we seriously start digging up all the domains and subdomains related to MXR Ads and Gretsch Politico. I’m sure we can find so much more than the three measly websites in a forgotten Gist paste. Hopefully we’ll land on a forlorn website with a sneaky vulnerability welcoming us inside.

We’ll begin our search by first checking certificate logs for subdomains.

# From Certificates

Censys (https://censys.io/) is a tool that routinely scans certificate logs to ingest all newly issued TLS certificates, and it’s number one on any pentester’s domain discovery tool list. Upon their issuance by a certificate authority, certificates are pushed to a central repository called a certificate log. This repository keeps a binary tree of all certificates, where each node is the hash of its child nodes, thus guaranteeing the integrity of the entire chain. It’s roughly the same principle followed by the Bitcoin blockchain. In theory, all issued TLS certificates should be publicly published to detect domain spoofing, typo-squatting, homoglyph attacks, and other mischievous ways to deceive and redirect users.

We can search these certificate logs to eke out any new registrations matching certain criteria, like “mxr ads.” The ugly side of this beautiful canvas is that all domains and subdomain names are openly accessible online. Secret applications with little security hiding behind obscure domains are therefore easily exposed. Tools like Censys and crt.sh explore these certificate logs and help speed up subdomain enumeration by at least an order of magnitude—a cruel reminder that even the sweetest grapes can hide the most bitter seeds. In Figure 4-7 we use Censys to search for subdomains of gretschpolitico.com.