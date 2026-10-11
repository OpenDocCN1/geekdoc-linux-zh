# CONFIGURING TRUSTS

Trust relationships allow two domains to share information. Windows 2000 makes trust relationships easier by implementing transitive trusts through the Kerberos security protocol. Windows 2000 domain controllers in the same domain, domain tree, or domain forest automatically trust each other through transitive trusts that are configured automatically. You can also establish trust relationships with other domains

that are not Windows 2000 Active Directory domains. This is performed by manually establishing the nontransitive trust on the Trusts tab of the domain properties. You must also manually establish a trust relationship for two Active Directory forests that want to communicate with each other. After you configure trust relationships, you can access the trust's properties sheets. You can use

the properties sheets to specify service principal name (SPN) suffixes, if desired. Servers identify themselves by using an SPN. Normally, this is the full DNS name of the server, but you can create different SPN suffixes for externally trusted domains so that the server does not have to reveal its full DNS name. This is a security feature of Windows 2000.

![](bbox=[0.07, 0.48, 0.48, 0.81])

![](bbox=[0.52, 0.48, 0.98, 0.81])

+   1 Select the domain you want to administer, and then choose Action>Properties.

+   2 To create a trust relationship, click Add to enter domains that trust and are trusted by your domain.
+   The Added Trusted Domain dialog box appears.

+   3 Type the trusted domain's name.
+   4 Type the password used to establish the trust relationship.

+   5 Retype the password to confirm.
+   6 Click OK