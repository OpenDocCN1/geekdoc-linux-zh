various problems with Evolution in the past in situations where Thunderbird has worked the first time.

# Evolution

To configure Evolution for LDAP, click the arrow next to the New button and select Address Book. A new screen appears, the first option of which prompts you for the type of address book to create. Select On LDAP Servers.

For Name, just enter Address book, and for Server, enter the IP address of your LDAP server (or 127.0.0.1 if you are working on the server), as shown in Figure 26.1. Leave the port as 389, which is the default for slapd. Switch to the Details tab, and set Search Base to be the DN for your address book—for example, ou=People,dc=hudzilla,dc=org. Set Search Scope to be Sub so that Evolution will perform a comprehensive search. To finish, click Add Address Book.

Although Evolution is now configured to use your directory, it will not use it for email address autocompletion just yet. To enable that, go to the Tools menu and click Settings. From the options that appear on the left, click Autocompletion and select your LDAP server from the list. Click Close, and then create a new email message. If everything has worked, typing part of someone's name should pop up a box with LDAP matches.

![](bbox=[0.08, 0.67, 0.43, 0.91])

FIGURE 26.1 Configuring Evolution to use LDAP for addresses is easy for anonymous connections.