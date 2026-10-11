# SETTING UP DNS CONTINUED

The Configure DNS Server Wizard asks you a number of questions to determine what place the DNS server has on the network. DNS needs to know if this is the first DNS server on the network. If it is not, then you have to enter the IP address of a known DNS server that currently exists.

You also need to decide whether you want to set up a forward lookup zone. You should allow DNS to create the forward lookup zone because this zone is used to forward and resolve IP to name mappings. The wizard recommends that you allow the service to create the forward lookup zone.

You also need to select the type of zone you want to create. You have the options of Active Directory integrated or a primary or secondary zone. An Active Directory integrated zone stores new zone database information in the Active Directory and provides secure updates to the database file. A standard primary zone stores the database file in a text file on the server so that the zone database information can be exchanged with other DNS servers that use text-based storage.

![](bbox=[0.04, 0.49, 0.48, 0.79])

![](bbox=[0.52, 0.49, 0.96, 0.79])

**4** Click the appropriate radio button.

**5** Click Next to continue.

**6** Click either the Yes or No radio button to create the forward lookup zone.

**7** Click Next to continue.