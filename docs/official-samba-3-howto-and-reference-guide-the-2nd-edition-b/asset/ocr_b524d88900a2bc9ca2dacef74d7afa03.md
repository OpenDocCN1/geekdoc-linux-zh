![](bbox=[0.08, 0.11, 0.88, 0.24])

# 4.6.2 Security Mode and Master Browsers

There are a few comments to make in order to tie up some loose ends. There has been much debate over the issue of whether it is okay to configure Samba as a domain controller that operates with security mode other than user-mode. The only security mode that will not work due to technical reasons is share-mode security. Domain and server mode security are really just a variation on SMB user-level security.

Actually, this issue is also closely tied to the debate on whether Samba must be the DMB for its workgroup when operating as a domain controller. In a pure Microsoft Windows NT domain, the PDC wins the election to be the DMB, and then registers the DOMAIN<1B> NetBIOS name. This is not the name used by Windows clients to locate the domain controller, all domain controllers register the DOMAIN<1C> name and Windows clients locate a network logon server for searching for the DOMAIN<1C> name. A DMB is a Domain Master Browser — see Chapter 9, “Network Browsing”, Section 9.4.1: Microsoft PDCs expect to win the election to become the DMB, if it loses that election it will report a continuous and rapid sequence of warning messages to its Windows event logger complaining that it has lost the election to become a DMB. For this reason, in networks where a Samba server is the PDC it is wise to configure the Samba domain controller as the DMB.

![](bbox=[0.08, 0.68, 0.88, 0.96])