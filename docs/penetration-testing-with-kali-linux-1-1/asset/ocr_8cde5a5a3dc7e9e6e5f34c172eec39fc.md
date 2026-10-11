> *all eight-character passwords may be tested within 2.5 hours and all nine-character passwords may be tested within 11 days.*

Next we will turn to Kerberos, which is the default authentication protocol in Active Directory and for associated services.

# ### 21.3.2 Kerberos Authentication

The Kerberos authentication protocol used by Microsoft is adopted from the Kerberos version 5 authentication protocol created by MIT and has been used as Microsoft’s primary authentication mechanism since Windows Server 2003. While NTLM authentication works through a principle of challenge and response, Windows-based Kerberos authentication uses a ticket system.

At a high level, Kerberos client authentication to a service in Active Directory involves the use of a domain controller in the role of a key distribution center, or KDC. ${ }^{644}$ This process is shown in Figure 310.

${ }^{644}$ (Wikipedia, 2017), https://en.wikipedia.org/wiki/Key_distribution_center