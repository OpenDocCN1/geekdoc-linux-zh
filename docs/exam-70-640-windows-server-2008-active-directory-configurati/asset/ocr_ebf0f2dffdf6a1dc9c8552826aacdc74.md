After completing this lesson, you will be able to discuss Group Policy management by focusing on planning an overall implementation strategy for GPOs within a Windows Server 2008 Active Directory environment. You will be able to use the Group Policy Management Console (GPMC), a unified management console that allows you to view GPO settings across an organization as well as report on existing GPO configurations and run “what-if” planning scenarios to test potential changes to your GPO environment. You will be able to fine-tune the application of GPOs using Security Group Filtering and WMI filters to better control which users and computers will (and will not) receive a particular GPO. You will troubleshoot GPOs, using built-in utilities such as the Resultant Set of Policy Wizard and Group Policy Modeling and Results queries.

# # Managing Group Policy

![](bbox=[0.11, 0.31, 0.95, 0.5])

This lesson focuses on expanding your knowledge of Group Policy. Specifically, you will learn how to plan and manage group policies. In addition to other management tools, we will discuss Group Policy Management, a new Windows Server 2008 MMC snap-in that can assist you in planning, implementing, and troubleshooting group policies. As you have learned, Group Policy is a powerful security tool that can provide administrative benefits when properly used and administered. It is important to be familiar with the tool and have a working ability to analyze and obtain information about applying Group Policy settings. As discussed in previous lessons, the policy-application process can be complex. When multiple policies are applied to a computer and to a user, it is important to understand which policy settings will be in effect after the policies have finished processing.

Although we have discussed the use of methods such as Block Policy Inheritance and Enforce to alter the flow of group policies within the Active Directory structure, several other methods can be used to filter policy application. These methods will be discussed in this lesson. In addition to defining policy-filtering methods, you will learn how to use various tools to identify the final effective GPO settings that are applied to a user or computer at any given time. Finally, we will discuss the key points to be considered when planning an effective Group Policy structure.

# ## Introducing the Group Policy Management MMC Snap-In

![](bbox=[0.32, 0.7, 0.94, 0.81])

The Group Policy Management MMC snap-in is a tool for managing Windows Server 2008, Windows Server 2003, and Windows 2000 Active Directory domains. The Group Policy Management MMC provides a single access point to all aspects of Group Policy that were previously spread across other tools, such as Active Directory Users and Computers, Active Directory Sites and Services, Resultant Set of Policy (Rsop), and the Group Policy Management Editor.

The simplified Group Policy Management user interface offers administrators a single point of administration for creating and modifying Group Policy. It also offers the following functionality:

+   *   **Importing and copying GPO settings to and from the file system.** This functionality works within a domain, across domains, or across forests. The Import Settings feature allows you to bring settings from a file system GPO into an existing GPO. The Copy feature allows you to copy settings from an existing GPO to a new GPO. Links to the