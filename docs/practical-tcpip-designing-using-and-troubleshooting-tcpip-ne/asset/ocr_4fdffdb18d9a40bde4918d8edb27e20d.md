# **17.7 LDAP – Lightweight Directory Access Protocol; overview**

Many applications on the network require information about users and other resources, e.g. user IDs and passwords are needed to control access to an application and its data. Some applications need more information, e.g. an e-mail client needs the user's full name, names of mail servers, and various other preferences; a calendar application needs the basic user information too, but also needs to know which department the user belongs to, which office they are in, and whether they are a manager (who can schedule meetings for their staff); the human resources (HR) application also needs to know the person's position in the organization, but in addition records more private information such as social security numbers, salary, etc.

This information is typically stored in some form of database specific to the application. Obviously, this gets complicated as more and more applications are added – one user ends up with multiple usernames and passwords in different places, and each application has its own isolated 'island' of information, often duplicating information used elsewhere by other applications (Figure 17.12). This imposes an ever-increasing maintenance load on the system administrators, and leads to errors or inconsistencies in the data.

![](bbox=[0.15, 0.39, 0.8, 0.59])

**Figure 17.12 Multiple applications duplicate lists of usernames, passwords etc**

*LDAP (Lightweight Directory Access Protocol)* begins to solve this problem. Instead of separate databases for each application, a single, central *directory* is maintained, containing all the information for all applications. This is made available as a network service (Figure 17.13), not as an application or file local to one machine.

All the applications now retrieve information from the one directory, using LDAP. For example, when a new employee joins the organization, the HR department creates a record for them in the directory, and the HR application automatically creates a username for them on the network and gives them access to the applications they need to perform their job, based on their department and job function. The organization's network starts to function as a single, integrated entity.

LDAP was originally implemented as a front-end to X.500 (which implemented the *Directory Access Protocol* (DAP), the directory service for OSI). However, X.500 is a big, heavyweight protocol, and when LDAP was implemented as a directory service in its own right, it was called *lightweight* in contrast. LDAP runs over TCP, on well-known port 389.

LDAP is used for storing information about all aspects and components of a network, not just users. Microsoft Windows-2000's Active Directory uses LDAP extensively, as does