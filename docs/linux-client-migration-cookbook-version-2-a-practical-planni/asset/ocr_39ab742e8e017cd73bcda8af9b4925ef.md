taken into account (that is, the UNIX groups the user belongs to and which are mapped to profiles play no role in that case).

Although all these rules are quite straightforward, a simple or even linear profile hierarchy is sufficient in most cases. For example, you can design the default user profile, add some features for a group needing more privileges, and so on. If there groups not fitting in this hierarchy (in our case, this could be the designer group), build their profile separately and either merge it with a profile in the first hierarchy or use it on its own.

A nice feature of the Kiosk Admin Tool is its remote configuration ability. Figure 7-2, you see how to map a local directory to a remote one (you can even change the base URL path. Files are transferred, for example, by the SSH protocol and the usual fish:// semantics or any other protocol that is supported by the KDE networking framework.

![](bbox=[0.271, 0.375, 0.747, 0.823])

Figure 7-2 Remote configuration with the Kiosk Admin Tool