
## The Parent Container

The **Parent Container** is created in the Internet Services container during installation. This container is the centralized location for Parent objects. NetMail Agents reference the Parent container when looking up user configuration information.

### Figure 8–4

![](img/d63035f3fce0eaaf97203dde900affb7_176_0.png)

A Parent object must be represented in the Parent container in order for NetMail Agents to find it. If a Parent object is created elsewhere in the tree, it must be represented by an Alias object in the Parent container.

## Templates

The Modular Web Agent provides 2 template-based, mail client interfaces:

- WebAccess
- WebMail

### Figure 8-5

The WebAccess interface provides standard mail client functionality as well as calendaring, scheduling, tasks, and notes. You can also use the WebAccess interface to give selected users access to NetMail administrative functions such as adding, modifying, and deleting user accounts.

![](img/d63035f3fce0eaaf97203dde900affb7_177_0.png)

### Figure 8-6

WebMail also provides standard mail client functionality; in addition, you can use the WebMail interface to give users access to self-administration features like changing passwords and configuring vacation messages.

![](img/d63035f3fce0eaaf97203dde900affb7_177_1.png)

Webacc.CTP and WebMail.CTP each contain everything needed to present their respective client interfaces; images, web pages, and localized text are all compiled in these 2 template files.

When the Modular Web Agent initializes on the messaging server, it simply loads the template files into memory.

The WebAccess and WebMail objects must be created in the tree before they can be loaded on the messaging server or selected in the Modular Web Agent, Parent, and User objects.

The *Template* container is created in the Internet Services container during installation. This container is the centralized location for template objects. The Modular Web Agent references the Templates container when scanning for available templates.

> A Template object must be represented in the Templates container for the Modular Web Agent to find it. If a Template object is created elsewhere in the tree, it must be represented by an Alias object in the Templates container.

## List Servers and Mailing Lists

The NetMail List Agent lets you create and maintain the following:

- List Server
- NDS Mailing Lists
- Mailing Lists Container

### List Server

A list server is a compilation of user email addresses. When a message is sent to the List server, the message is automatically forwarded to every user who has subscribed to the list.

List User objects represent the members of a list. When users subscribe to a list, a List User is added to the respective Mailing List object.

You can also add list members by creating List User objects within the Mailing List object.

### NDS Mailing Lists

NDS mailing lists allow you to send messages to eDirectory users.

Unlike Mailing Lists, NDS Mailing Lists are made up of eDirectory objects rather than user email addresses. Selected eDirectory objects can include

- Container objects
- Groups
- Organizational roles
- Aliases
- User objects

If a container object is selected, messages are forwarded to the users within the designated Container object.

### Mailing Lists Container

The Mailing Lists container is created in the Internet Services container during installation. This container holds all of the messaging system's available Mailing List objects.

The List Agent references the Mailing Lists container when scanning the message queue for messages addressed to mailing lists.

A Mailing List object must be represented in the Mailing Lists container in order for the List Agent to find it. If a Mailing List object is created elsewhere in the tree, it must be represented by an Alias object in the Mailing Lists container.

## NetMail Agents

*NetMail agents* are a set of executables that perform specific product functions. These agents have plug-and-play versatility. They can be combined in a variety of configurations and still maintain the functionality of a single, integrated messaging system.

![](img/d63035f3fce0eaaf97203dde900affb7_180_0.png)

This building block architecture enables NetMail to be easily distributed across multiple servers. Depending on agent usage and system resources, each agent can run by itself or in conjunction with other agents on a messaging server.

### Table 8-1

The table below lists all the NetMail agents and summarizes their functions in the NetMail system.

| Agent | Function |
| :--- | :--- |
| **Address Book Agent** | The Address Book Agent provides read-only LDAP access to eDirectory. Using this agent, any LDAP3-compliant application (such as email or address book clients) can access address book information from eDirectory. |
| | Information returned about each user depends on the user’s privacy level. |
| **Alias Agent** | The Alias Agent enables your NetMail system to recognize user aliases. The Alias Agent can also be used to automatically populate the User object's Internet E-mail Address property. |
| | The automatic aliasing feature pulls information directly from eDirectory to generate aliases for eDirectory User objects. Aliases can be automatically generated in the following formats: <br> - Firstname_Lastname@Domain <br> - First Letter+Lastname@Domain (This alias option is limited to eight characters.) <br> - Firstname.Lastname@Domain <br> - First.M. Last@Domain <br> - First_M_Last@Domain <br> <br> The aliases created via the Alias Agent are not defined as Alias objects in eDirectory. They are maintained by the Alias Agent and are specific to the NetMail message system. <br> <br> Existing Alias objects are recognized by NetMail, but they function independently of the Alias Agent. Messages addressed to Alias objects are automatically delivered to the associated user's mailbox by the NMAP Agent. <br> <br> Aliases can also be defined manually. |
| **AntiSpam Agent** | The AntiSpam Agent automatically lets you build a blackout list of undesirable email domains and addresses. <br> <br> Messages sent from domains and email addresses contained in the blackout list are not accepted by the NetMail system. |
| **AntiVirus Agent** | The NetMail AntiVirus Agent integrates with the following virus applications to provide virus scanning on messages handled by NetMail:<br> - McAfee® NetShield®<br> - Command® Antivirus<br> - Computer Associates® InnoqualeIT®<br> - Symantec® CarrierScan™<br><br>You must install one of these products before you can use NetMail’s AntiVirus Agent.<br><br>If a message contains a virus, the AntiVirus Agent immediately deletes it from the message queue.<br><br>It can be configured to return the message to the sender with a notice indicating what virus the message contained.<br><br>It can also send a virus alert to the intended message recipients indicating who tried to send the message and what virus the message contained.<br><br>Virus scanning can be enabled for all users in the messaging system or it can be limited to a group of users.<br><br>Virus scanning is enabled at the Parent or User objects. |
| **AutoReply** | The AutoReply Agent lets users create custom messages that are automatically sent in response to incoming mail. |
| | For example, when users go on vacation, they can create a message that lets others know they are unavailable. |
| | The AutoReply Agent also enables users to forward their messages to another email address. Users can specify if they want to retain a copy of the message in their NetMail mailbox or simply redirect the message to the designated address. |
| | In addition to forwarding messages to another email address, the AutoReply Agent can forward SMS messages to cellular phones and pages. |
| | The AutoReply Agent is not email client specific. Users’ forward and autoreply information is stored in their User objects. |
