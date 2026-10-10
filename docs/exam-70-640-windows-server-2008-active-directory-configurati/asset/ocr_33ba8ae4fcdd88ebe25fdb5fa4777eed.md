# Fill in the Blank
Complete the following sentences by writing the correct word or words in the blank provided.
1. The Active Directory domain is viewed as one domain controller to its ______.
2. Active Directory ______ is a container-like security boundary for an Active Directory environment.
3. The flexible file reference, Active Directory contains two ______ replication model.
4. ______ (a ______ relationship with X in X's data base are well-organized.)
5. The ______ existing server is replaced across the domain.
6. ______ of a basic Active Directory domain database is located within the 
   directory structure.
7. A ______ provides a view for naming tree relationships between all
   domains within two forest trees.
8. Each domain in an Active Directory forest has a ______ that relationship
   with other server domains in a forest.
9. ______ allows a user in a resource to be able to use log into Active Directory
   without needing to connect multiple times.
10. Active Directory allows you to ______ a DNS to isolate Active Directory
   resources such as domain controllers and global catalog servers.

+   ### Multiple Choice
+   Circle the correct answer.
+   1. Which of the following items is a child object in Active Directory?
+      a. OUs
+      b. Users
+      c. Application policies
+      d. OU
+   2. Which of the following events can be logged in a forest that is entirely on or the
+      Windows Server 2008 forest functional level?
+      a. Windows 2000
+      b. Windows 2003
+      c. Windows 2008
+      d. Windows NT 4.0
+   3. You are planning on for Active Directory implementation for a company that currently
+      has Windows, operating system environment. All department-level units are to be
+      created and managed in Active Directory. What feature will likely be most useful to
+      Active Directory in allow each manager to manage their own department?
+      a. OUs (Organizational Units)
+      b. Delegation of control
+      c. Build-Out (Organizational Control)
+      d. Hierarchical replication
+      e. GPOs (Group Policies)
+      f. Active Directory trust model
+   4. Which is required to test for Active Directory to function:
+      a. One or more forest servers
+      b. One or more forest support
+      c. One or more DCs
+      d. Active Directory integration

+   6. You are trying to add an Active Directory child domain from a subdomain in
+      Microsoft's 17th location. In practice, which two statements are true regarding the
+      addition of the domain:
+      a. The FDC Controller is the child database
+      b. The FDC controller is the parent database
+      c. An external object that authenticates the workforce
+      d. An internal object that authenticates the workforce
+   8. Each FDC/FSMO role container is two components the domain portion and the 
+      domain FDC. The portion of the FDC/FSMO role container that is called:
+      a. Domain Authority Unit (DAU)
+      b. Active Directory Domain and Computers
+      c. Active Directory Forest and Forest
+      d. Active Directory Domain and Trusts

# Case Scenarios

**Scenario 6-1: FSMO Role Placement—I**
Given as a precondition to this exercise is a 15-employee IT department. The manager, 
Kempkin, has a total of two domain controllers in the forest. In this scenario, 
one of the two must be decommissioned. Kempkin wants to ensure that the 
FDC/FSMO roles are properly placed in the remaining domain controller, so that 
the network can continue to function as expected. Based on the information 
provided, which of the five roles should Kempkin place on the remaining domain 
controller, and why?

**Scenario 6-2: FSMO Role Placement—II**
Given as a precondition to this exercise is a five-domain forest with the 
following domains: contoso.com, contoso.local, contoso.org, contoso.net, 
and contoso.co.uk. You need to determine which of the domain controllers 
in the forest should be the PDC Emulator, RID Master, and Schema Master 
roles. Which domain controller should have each of these roles, and why?

# Knowledge Assessment Questions

# Workplace Ready Project

![](bbox=[0.5, 0.33, 0.95, 0.34])

# Use Repadmin to Query Domain Controllers

Domain Manager in the Active Directory administration for Microsoft Windows 
Systems.
1. At command prompt, enter the following command to list all domain 
controllers in the Active Directory:
   ```
   ntdsutil quads show dcs
   ```
2. Note how the following command lists all domain controllers in the 
   domain:
   ```
   repadmin /showrepl
   ```
3. Run the following command to query a specific domain controller:
   ```
   repadmin /showrepl <DNS hostname of DC>
   ```

The following text is excerpted from Windows Server 2003 Active Directory:
"Windows Server 2003, domain system. The domain system contains the 
Active Directory domain system and the domain. It may be necessary to 
query a specific domain controller to get information about its 
replication partners and the replication status of its directory partitions. 
Use the following command to query the replication status of the domain 
controller: `repadmin /showrepl`"

+   - **Windows Server 2003** : **2003**  
+     - **Windows Server 2003** : **2003**  
+       - **Windows Server 2003** : **2003**  
+         - **Windows Server 2003** : **2003**  
+           - **Windows Server 2003** : **2003**  
+             - **Windows Server 2003** : **2003**  
+               - **Windows Server 2003** : **2003**  
+                 - **Windows Server 2003** : **2003**  
+                   - **Windows Server 2003** : **2003**  
+                     - **Windows Server 2003** : **2003**  
+                       - **Windows Server 2003** : **2003**  
+                         - **Windows Server 2003** : **2003**

The previous command output is an example of the replication relationships in the 
two-part domain controller that has 25 domain controllers and 25 domain controllers. The 
replication relationships in this domain are configured as follows: Domain System 
2000, which is an active replication relationship between the domain 
controllers. Use the following command to query a specific domain controller:

www.wiley.com/colllege/microsoft or 
call the MOAC Toll-Free Number: 1+(888) 764-7001 (U.S. & Canada only)