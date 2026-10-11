# MANAGING ZONE RESOURCE RECORDS AND DELEGATION

# Zone Delegation

As with many Windows 2000 components, both within the Active Directory and the operating system, you can delegate control. Delegation means that you allow another user, group, or computer to control some object, group, process, or service. Delegation is a concept you learn to use throughout the rest of the book

in relation to Active Directory objects, OUs, services, and so on.

You can choose to delegate control of a zone to another DNS server in another zone. This action allows another DNS server(s) to have authority of a particular zone. When

you perform this action, however, you must also create delegation records in the other DNS zones that point to the DNS servers that have authority over the new zone. This allows the transfer of authority to take place and provides a correct reference to the other DNS servers that the zone has been delegated to.

![](bbox=[0.02, 0.5, 0.49, 0.81])

1 Select the appropriate zone in the console and choose Action>New Delegation.

![](bbox=[0.5, 0.5, 0.98, 0.81])

The New Delegation Wizard appears.

2 Click Next to continue.