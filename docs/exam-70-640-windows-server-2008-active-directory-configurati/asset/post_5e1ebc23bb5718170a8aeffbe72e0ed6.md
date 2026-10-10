
# Case Scenarios

## Scenario 8-1: Lucerne Publishing and Offline Files

You are a computer consultant. Linda Randall, Chief Information Officer of Lucerne Publishing, has asked for your help. The Lucerne Publishing network consists of a single Active Directory domain with four domain controllers running Windows Server 2008, three file servers, and 300 clients that are evenly divided between Windows XP Professional and Windows Vista.

Recently, several publishing projects stored in electronic format were lost when an employee’s laptop was stolen from a publishing convention. Previously, another employee lost important publishing project files during a fire sprinkler system incident in which the employee’s computer was destroyed.

Employees typically store documents in the Documents folder on their local systems. Linda wants all employees to store their data on the network servers. The data on the network servers is backed up regularly. Linda tells you that her editors tend to work on sensitive data that requires special handling. She is especially worried that the data is backed up and secured.

All client computers have P drive mappings that are supposed to be used for storing files. However, many employees do not understand drive mappings. They often store files in their Documents folder and then copy them over to the P drive. This is also an issue because many employees forget to copy their files to the server until something occurs, such as a data loss.

Given Lucerne Publishing’s concerns, answer the following questions:

- a. How would you address Linda’s concern that some employees do not understand drive mappings and others forget to store their data on the server?
- b. How can you address the situation concerning the sensitive data editors use?
- c. How would you address the users with mobile computers so that they could work on their files while traveling?
- d. Linda warns that some users may have huge amounts of data already stored in the My Documents folder on their local computer. How might this affect your recommendations?

# Performing Software Installation with Group Policy

## OBJECTIVE DOMAIN MATRIX

| TECHNOLOGY SKILL | OBJECTIVE DOMAIN | OBJECTIVE DOMAIN NUMBER |
|---|---|---|
| Managing Software through Group Policy | Configure software deployment GPOs. | 4.5 |

![](img/a8ee53dbf1310726255b6fbb9f296fb2_222_0.png)

- Assign
- Basic User
- certificate rule
- Disallowed
- distribution share
- file-activated installation
- hash
- hash algorithm
- hash rule
- hash value
- Install This Application At Logon
- .msi file
- network zone rule
- patch files
- path rule
- Publish
- repackaging
- self-healing
- software life cycle
- System Development Life Cycle (SDLC)
- Unrestricted
- .zap file

Lucerne Publishing has created a series of GPOs to configure password and account lockout policies and similar security-related settings on the Lucerne Publishing corporate network. Management wants to extend Active Directory to further automate the desktop management process by allowing automated software deployments. Certain applications are required across the entire enterprise; the layout artists and graphic designers use different graphics applications that they switch between, depending on the needs of a particular project. Finally, Lucerne Publishing's Human Resources department wants to restrict the use of peer-to-peer file sharing applications on the Lucerne Publishing network because of copyright and intellectual property issues.

After completing this lesson, you will be able to discuss the tasks necessary to configure Software Installation via Group Policy. This includes the steps needed to package software installers into a format that can be leveraged by Group Policy Objects, as well as determining the appropriate means of deploying software installation GPOs within your organization. You will also be able to deploy Software Restriction Policies (SRPs) to control which software can and cannot be installed and run from user workstations and servers within an Active Directory domain.

# Managing Software through Group Policy

**THE BOTTOM LINE.**

Group Policy can be used to install, upgrade, patch, or remove software applications when a computer is started, when a user logs on to the network, or when a user accesses a file associated with a program that is not currently on the user's computer. In addition, Group Policy can be used to fix problems associated with applications. For example, if a user inadvertently deletes a file from an application, Group Policy can be used to launch a repair process that will fix the application. To understand how Group Policy can be used to perform all of these tasks, we will discuss the Windows Installer Service and its purpose. We will also discuss Software Restriction Policies, their benefits, and how you configure them to meet the needs of your organization.

The process that takes place from the time an application is evaluated for deployment in an organization until the time when it is deemed old or not suitable for use is referred to as the *software life cycle*. The software life cycle is a derivative of the *System Development Life Cycle (SDLC)*. The SDLC is used to develop information systems software, projects, or components through a structured process that includes analysis, design, implementation, and maintenance. The software life cycle consists of four phases that are derived from the SDLC model, as follows:

- **Planning.** This phase defines all planning activities, including the analysis of the software to be installed, verification of its compatibility, supported methods of installation, and the identification of any risks associated with the software and the desired deployment method.
- **Implementation.** This phase is used to prepare for deployment. Using Group Policy as a tool, the implementation phase includes a set of steps for a deployment, such as creating a shared access location for files and creating or using the appropriate package files. After all of the deployment steps have been achieved, the actual deployment takes place in this phase.
- **Maintenance.** The maintenance phase includes the elements that are required to keep the software running smoothly. Examples of this include upgrading software to the latest version, installing patches when necessary, and a *self-healing* function that allows the software to detect and correct problems such as missing or deleted files.
- **Removal.** The removal phase is the final phase before the software life cycle begins again with a new software deployment plan. When software is scheduled to be retired due to obsolescence or software requirement changes, this phase requires a clean removal of the software to be performed.

This lesson describes how Group Policy can be used to accomplish the latter three phases. Understanding how to use Group Policy to implement, maintain, and remove software is extremely helpful in streamlining the management of software across your enterprise.

Microsoft Windows Server 2008 uses the Windows Installer with Group Policy to install and manage software that is packaged into an .msi file. Windows Installer consists of two components: one for the client-side component and another for the server-side component. The client-side component is called the *Windows Installer Service*. This client-side component is responsible for automating the installation and configuration of the designated software. The Windows Installer Service requires a package file that contains all of the pertinent information about the software. This package file consists of the following information:

- An .msi file, which is a relational database file that is copied to the target computer system with the program files it deploys. In addition to providing installation information, this database file assists in the self-healing process for damaged applications and clean application removal.
- External source files that may be required for the installation or removal of software.
- Summary information about the software and the package.
- A reference point to the path where the installation files are located.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_223_0.png)
