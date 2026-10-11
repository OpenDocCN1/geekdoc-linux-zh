# ### 3.5.2 What Makes Samba a Domain Controller?

The smb.conf parameter *security = domain* does not really make Samba behave as a domain controller. This setting means we want Samba to be a domain member. See Chapter 4, “Domain Control” for more information.

# ### 3.5.3 What Makes Samba a Domain Member?

Guess! So many others do. But whatever you do, do not think that *security = user* makes Samba act as a domain member. Read the manufacturer’s manual before the warranty expires. See Chapter 6, “Domain Membership”, for more information.

# ### 3.5.4 Constantly Losing Connections to Password Server

“Why does server_validate() simply give up rather then re-establish its connection to the password server? Though I am not fluent in the SMB protocol, perhaps the cluster server process passes along to its client workstation the session key it receives from the password server, which means the password hashes submitted by the client would not work on a subsequent connection whose session key would be different. So server_validate() must give up.”

Indeed. That’s why *security = server* is at best a nasty hack. Please use *security = domain*; *security = server* mode is also known as pass-through authentication.