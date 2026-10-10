+   c.  500
+      d.  1,000

+   8.  You are logging on to an Active Directory child domain from a workstation running Windows Vista Business. By default, where will this workstation look to synchronize its clock with the domain?
+      a.  The PDC Emulator for the child domain
+      b.  The PDC Emulator for the forest root domain
+      c.  An external clock
+      d.  The domain controller that authenticates the workstation

+   9.  Each object’s SID consists of two components: the domain portion and the \_\_\_\_\_\_\_\_\_.
+      a.  remote identifier
+      b.  globally unique identifier
+      c.  relative identifier
+      d.  global identifier

+   10. You can view and manage the PDC Emulator FSMO role holder using which utility?
+      a.  Active Directory Users and Computers
+      b.  Active Directory Schema
+      c.  Active Directory Sites and Services
+      d.  Active Directory Domains and Trusts

# Case Scenarios

# **Scenario 4-1: FSMO Role Placement—I**

Contoso Pharmaceuticals has 500 employees in 14 locations. The company headquarters is in Hartford, Connecticut. All locations are part of the contoso.com domain, contain at least two servers, and are connected by reliable links.

+   a.  Which FSMO roles would you house at the Hartford location?
+      b.  While trying to add new user accounts to the domain, you receive an error that the accounts cannot be created. You are logged on as a member of the Domain Admins group. What is most likely causing the problem?
+      c.  What should you consider placing at each location to facilitate logons?

# **Scenario 4-2: FSMO Role Placement—II**

Contoso Pharmaceuticals is expanding to include several newly acquired companies. Although they will each become part of the contoso.com forest, each of these companies wants to maintain their own decentralized management strategy. To accommodate this request, you have installed the subsidiaries as separate domain structures. One of them is named litwareinc.com.

+   a.  Which roles will this new domain need to accommodate?
+      b.  If litwareinc.com decides to have a small satellite office included in their domain for several users without having logon traffic using their available bandwidth to the parent domain, what should they do?
+      c.  In contoso.com, your server functioning as the Domain Naming Master has failed due to a power surge. You are unable to create a new child domain for a new location until this server is back online. Currently, it is not expected that the Domain Naming Master issue will be resolved in a reasonable amount of time. What steps should you take so that you can resolve this problem and create the necessary child domain?