+   10. What can be used to run script files using VBScript or JScript from the Windows desktop or from a command prompt?
+   a. Visual Basic
+   b. Windows Scripting Host (WSH)
+   c. Visual Basic Express
+   d. Windows Scripting Engine

# ■ Case Scenarios

# Scenario 5-1: Administering Groups for Humongous Insurance

You are a network administrator for Humongous Insurance. Humongous Insurance has a multidomain forest. The forest root is humongousinsurance.com. There are also two child domains named west.humongousinsurance.com and east.humongousinsurance.com. The company has approximately 7,000 users, 7,000 client workstations, and 100 servers.

All domains are Windows Server 2008 domains. The forest root domain has 10 domain controllers. Five of those domain controllers are configured as DNS servers and two are configured as global catalog servers. The West domain has three domain controllers. Two of those domain controllers are configured as DNS servers. One of those domain controllers is configured as a global catalog server. The East domain has two Windows Server 2008 domain controllers and three Windows 2003 domain controllers.

The forest root domain is located in College Station, Texas. The East domain is located in Gainesville, Florida. The West domain is located in San Diego, California. An Active Directory site is configured for each of these locations. The site for College Station is named Main_Site. The Gainesville site is named East_Site. The San Diego site is named West_Site.

You are one of several network administrators assigned to handle the forest root domain and College Station site. Your manager, Jean T'renary, has called a meeting of all network and desktop administrators. She wants to address several issues.

+   1. Jean says four internal auditors are in the forest root domain. Two internal auditors are in each of the child domains. Each set of internal auditors has been placed in a global group within each domain. These groups are named IA_Main, IA_East, and IA_West after their respective locations. Jean wants all of the members of these groups to be able to access a common set of resources in the Main domain, while still segregating the auditors' ability to access other resources in domains other than their own. What is the recommended way to configure the groups to allow the desired functionality?
+   2. The network administrators from the West domain want to know why everyone always recommends placing global groups into universal groups instead of placing the users directly into the universal groups. What should you tell them?
+   3. Jean approves a plan to hire assistants for each domain to create and manage user accounts. How can you give the assistants the immediate ability to help in this way without making them domain administrators?
+   4. Two employees have been hired to back up data and manage printers for the Main_Site. Which built-in groups will give these users the permissions they require to manage the domain controllers? How should you set up their accounts and group memberships?

# Scenario 5-2: Evaluating Scripts

> *This scenario will help you to find and evaluate one of the script types discussed in this lesson.*

+   1. Describe each type of scripting that can add users to Active Directory. Provide an example of a scenario using each one.
+   2. Using the Internet as your resource, find an example of one of the script types and write a short description of the script and what it accomplishes.