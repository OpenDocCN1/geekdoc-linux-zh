the Lab OU will be applied. This resolves the issue of applying unwanted settings on shared computers from other locations in the Active Directory hierarchy.

# **SUMMARY SKILL MATRIX**

+   **IN THIS LESSON YOU LEARNED:**
+   
+   *   Group Policy consists of user and computer settings that can be implemented during computer startup and user logon. These settings can be used to customize the user environment, to implement security guidelines, and to assist in simplifying user and desktop administration. Group Policies can be beneficial to users and administrators. They can be used to increase a company's return on investment and to decrease the overall total cost of ownership for the network.
+   *   In Active Directory, Group Policies can be assigned to sites, domains, and OUs. By default, there is one local policy per computer. Local policy settings are overwritten by Active Directory policy settings.
+   *   Group Policy content is stored in an Active Directory GPC and in a GPT. Whereas the GPC can be seen by using the Advanced Features view in Active Directory Users and Computers, the GPT is a GUID-named folder located in the systemroot\sysvol\SYSVOL\*domain_name*\Policies folder.
+   *   The Default Domain Policy and the Default Domain Controller Policy are created by default when Active Directory is installed.
+   *   The Group Policy Management Console is the tool used to create and modify Group Policies and their settings.
+   *   GPO nodes contain three subnodes, including Software Settings, Windows Settings, and Administrative Templates. Administrative templates are XML files with the .admxx file extension. Over 100 ADMX files are included with Windows Server 2008.
+   *   The order of Group Policy processing can be remembered using the acronym LSDOU: local policies are processed first, followed by site, domain, and, finally, OU policies. This order is an important part of understanding how to implement Group Policies for an object.
+   *   Group Policies applied to parent containers are inherited by all child containers and objects. Inheritance can be altered by using the Enforce, Block Policy Inheritance, or Loopback settings.

# ## **Knowledge Assessment**

# **Matching**

*Match the following definitions with the appropriate term.*

+   a.  Administrative Templates
+   b.  asynchronous processing
+   c.  Block Policy Inheritance
+   d.  Default Domain Controller Policy
+   e.  Enforce
+   f.  GPO Inheritance
+   g.  local GPO
+   h.  Loopback Processing
+   i.  LSDOU
+   j.  multiple local GPOs

+   ________ 1.  Configuring this setting will prevent a GPO's settings from being overwritten by another GPO that is applied later in the inheritance process.
+   ________ 2.  By default, GPOs are applied in this order.
+   ________ 3.  Computers in child OUs will receive GPO settings applied to a parent OU through this process.
+   ________ 4.  User logon scripts are applied in this manner.
+   ________ 5.  These are used to define registry-based policy settings in the User Configuration and Computer Configuration nodes.