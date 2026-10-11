
### Calendar Agent
In this situation, NetMail simply delivers the appointments as messages to the clients and doesn't process them as calendar items.

If you are deploying the NetMail web interface, however, you must deploy the Calendar Agent if you want users to be able to send and receive appointments. The configurable property of the Calendar Agent object in your tree is minimal, as shown in Figure 10.4.

![](img/c7771e8540507f2b00c088c7a411b57b_456_0.png)

### The Connection Manager Agent
This agent is used by the NetMail system to keep track of users who have authenticated to the system. The POP and IMAP Agents (discussed later) forward authenticated users' IP addresses to the Connection Manager Agent. This information is used by other NetMail agents to prevent the system from being used to relay email messages.

> **NOTE**
> Email relay occurs when an unauthorized third party uses your SMTP service to send email messages. This effectively spoofs the origin of the email, leading recipients to believe the message originated from your organization. This strategy is frequently used by shady email spammers to conceal the real origin of their messages.

The Connection Manager Agent runs on IP port 689. Because of the risk of relayers, Novell recommends that the server hosting the Connection Manager Agent be situated behind your organization's firewall. The Connection Manager Agent object attribute is shown in Figure 10.5.

![](img/c7771e8540507f2b00c088c7a411b57b_457_0.png)

![](img/c7771e8540507f2b00c088c7a411b57b_457_1.png)

### The IMAP Agent
The IMAP Agent is used to allow users to access their mailboxes in the NetMail system with a client using the IMAP 4 protocol.

> **NOTE** IMAP stands for Internet Message Access Protocol. IMAP is a protocol used to download messages from an email server. IMAP allows you to store your email messages on the email server and/or download them to the local email client. IMAP also provides you with the ability to download only the message header from the server to the client, allowing you to determine whether you want to download the entire message. IMAP allows you to maintain multiple folders on the server and move email messages between them. IMAP uses IP port 143.

According to Novell, each concurrent IMAP connection to your NetMail server consumes about 300KB of RAM. To keep your system functioning smoothly, you should try to anticipate the load that will be placed on your server by the IMAP Agent and add RAM to accommodate it. The attribute of the IMAP Agent object is shown in Figure 10.6.

![](img/c7771e8540507f2b00c088c7a411b57b_458_0.png)

### The List Server Agent
The List Server Agent allows your NetMail server to function as a list server. You can use this agent to service lists generated manually or generated using eDirectory objects. For example, you could generate a list using the iFCLE organizational unit in your tree. All users in the container would be included in the list. New users added later to the container would be added dynamically to the list.

**Figure 10.6**
IMAP Agent object property.

### The Modular Web Agent
As mentioned previously, NetMail can be used with standard email client software or with its own web-based user interface. The Modular Web Agent is the service that provides this interface. It runs on IP port 52080 (insecure) and port 52443 (secure).

The Modular Web Agent employs two default templates used to create the web interface. These are the WebMail and WebAccess templates. If you have a little programming experience, you can modify these templates to customize the appearance of these interfaces.

As with the IMAP Agent, the Modular Web Agent consumes about 300KB of RAM for each concurrent session. You should calculate the load that will be placed on your Modular Web Agent and add RAM to your system accordingly. The properties of the Modular Web Agent object are shown in Figure 10.7.

### The NMAP Agent
The Network Messaging Application Protocol (NMAP) Agent is the heart of the NetMail system. Its primary job is the processing of messages through the NetMail system. Unlike many of the other NetMail agents, the NMAP Agent is not optional. You must have at least one NMAP Agent running in your network for the NetMail system to function.

**Figure 10.7**
Modular Web Agent object properties.

![](img/c7771e8540507f2b00c088c7a411b57b_459_0.png)

The NMAP Agent is the only NetMail agent that has access to the message store directory in the Linux server's file system. The NMAP agent maintains a mailbox for each NetMail user.

The NMAP Agent is also the only NetMail agent that has access to the message queue in the Linux file system. Every message waiting to be processed is stored in this queue.

All other NetMail agents access the message store or the message queue through the NMAP Agent. For example, if the IMAP Agent needs to retrieve a message from a user's mailbox, it contacts the NMAP Agent, which processes the request on behalf of the IMAP Agent.

Because the NMAP Agent requires access to the file system, it must be deployed on the same server where the message store and message queue are located. The attributes of the NMAP Agent object are shown in Figure 10.8.

### The POP Agent
The POP Agent allows email clients to access user mailboxes using the POP3 protocol.

> **NOTE** Like IMAP, POP3 is an email protocol used to retrieve messages from an email server. Unlike IMAP, POP3, by default, always deletes the message from the email server when it is downloaded to an email client. It also only allows a single folder on the email server for each user. POP3 runs on IP port 110.

**Figure 10.8**
NMAP Agent object properties.

![](img/c7771e8540507f2b00c088c7a411b57b_460_0.png)

As you may have gathered from the preceding discussion, the NetMail system can't deliver messages to clients unless an agent specific to the protocol used by the clients has been deployed. For example, if you want users to have IMAP access to their mailboxes, you must deploy the IMAP Agent. If you want them to have access to their mailboxes using POP3, you must deploy the POP Agent. If you don't implement either of these, users won't be able to access their mailboxes using email client software.

If you only want users to be able to access their mailboxes using NetMail's web interface, you only need to deploy the Modular Web Agent. The IMAP and POP Agents aren't required to use the Modular Web Agent. The property of the POP Agent object is shown in Figure 10.9.

### The Proxy Agent
The Proxy Agent is a useful agent that allows users to configure their NetMail mailbox to retrieve email from up to three other email accounts external to the NetMail system using the POP3 or IMAP protocol. Messages retrieved from the external accounts are stored in and can be retrieved from the user's NetMail mailbox. The attributes of the Proxy Agent object are shown in Figure 10.10.

**Figure 10.9**
POP Agent object property.

![](img/c7771e8540507f2b00c088c7a411b57b_461_0.png)

**Figure 10.10**
Proxy Agent object properties.

![](img/c7771e8540507f2b00c088c7a411b57b_461_1.png)

### The SMTP Agent
The SMTP Agent has two main roles in the NetMail system. First, whereas the IMAP and POP3 Agents are used to transfer messages from the NetMail server to remote email clients, the SMTP Agent's job is to allow messages to be sent from email client software to the NetMail server.

> **NOTE** SMTP stands for *Simple Mail Transfer Protocol*. The SMTP protocol supports both sending and receiving email messages; however, its receiving capabilities are very limited. Therefore, it is usually deployed in conjunction with IMAP and/or POP3. SMTP is used to send mail, whereas IMAP or POP3 is used to receive mail. SMTP runs on IP port 25.

If you don't implement an SMTP Agent, users who employ email client software, such as Outlook, won't be able to send messages. Its second job is to function as an interface between the NetMail system and the external network (including the Internet). Messages sent by NetMail users to other internal NetMail users are delivered by the NMAP Agent. However, if a NetMail user sends a message to an external recipient, the SMTP Agent is employed to send the message over the Internet to the destination mail server.

The SMTP Agent can be configured with a variety of settings that restrict the host domains that messages can be sent to, limit the maximum message size allowed, and perform reverse DNS lookups. The properties of the SMTP Agent object are shown in Figure 10.11.

![](img/c7771e8540507f2b00c088c7a411b57b_462_0.png)

As mentioned, each of these agents is represented by an object in your eDirectory tree. All configuration parameters for each are stored as attributes of the object.

The NetMail installation also adds several other objects to your eDirectory tree. Let's look at each.

## NetMail Objects Added During Installation

During the installation of NetMail, the schema of your eDirectory tree is extended and several new object classes are added. Corresponding objects
