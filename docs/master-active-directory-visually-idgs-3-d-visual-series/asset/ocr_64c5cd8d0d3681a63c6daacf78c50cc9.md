# TIPS

# What is a zone?

A zone is an area of the DNS namespace that is segmented for administrative purposes. This zone method enables you to run different DNS servers on your network that service the needs of particular groups. For example, if you had an **hr.corp.com** division and an **acct.corp.com** division in your network, each of these could function as DNS zones. They apply to a discreet portion of the namespace and you can set up different DNS servers to manage each zone. This feature keeps query traffic more localized on the network because all computers within a zone have to contact a DNS zone server for queries.

# Why is a wizard provided to set up DNS?

Windows 2000 includes wizards for most tasks that require several steps or several “pieces” that must be configured. The wizard makes certain you enter all the information needed to appropriately configure the service.

![](bbox=[0.02, 0.51, 0.46, 0.79])

![](bbox=[0.5, 0.51, 0.94, 0.79])

+   **1** Choose **Action** Configure The Server.

+   **2** The Configure DNS Server Wizard appears.

+   **3** Click Next to continue.