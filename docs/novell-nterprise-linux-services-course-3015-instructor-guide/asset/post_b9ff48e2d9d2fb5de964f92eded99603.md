
i. (Conditional) If your container is not listed, add **your container** (by using the magnifying glass icon); then select **Save**.

4. Verify that your POP Agent is enabled:
   - a. Under **DAx Messaging Server**, select **POP Agent**.
   - b. Verify that the agent is enabled
   - c. (Conditional) If the agent is not enabled, select **Enabled** and then select **Save**.

5. Set the server time zone:
   - a. On the left, select **Modular Web Agent**.
   - b. On the right from the Default Time Zone drop-down list, select **your time zone**. You do this to make sure the Messaging Server's time zone is the same as the NNLS server's time zone.
   - c. Select **Save**.

6. Test the configuration.
   - a. From the current Mozilla web browser window, open a new browser window by pressing **Ctrl+N**.
   - b. Enter **http://DAx.your container.digitalairlines.com:52080**.
   - c. When prompted to log in, enter **JJackson** with a password of **novell**; then select **OK**. A WebAccess page appears.
   - d. At the left, select the **Compose** icon.
   - e. In the To field, enter **AGresko@your container.digitalairlines.com**. For example, if you're working on DA3, you would enter **AGresko@atl.digitalairlines.com**.
   - f. Enter *text* in the Subject and Message fields.

If you leave the Message field empty, the message won’t be sent.

   - g. Select **Send**.
   - h. Wait for the Send window to close; then, at the top of the Web/Access page, select the **Exit** icon.
   - i. Select **Log in**.
   - j. When prompted to log in, authenticate as **AGresko** with a password of **novell**.
     You should see the message you just sent from the other account.
   - k. Select the *message*.
   - l. Try sending email to other users in your tree.
   - m. Try sending an email message to a user in another tree.
   - n. When you finish, close the browser windows.

*(End of Exercise)*

## Summary

| Objective | Summary |
| :--- | :--- |
| **1. Identify NetMail Features** | Novell NetMail is a high-performance e-mail and calendaring system based on Internet-standard messaging and security protocols. |
| | NetMail is designed to fit multiple network environments. It has been tested successfully with as many as 30,000 users on a single Linux server. |
| | NetMail's highly efficient distributed architecture minimizes the number of servers you need to run your e-mail and calendaring system. |
| | NetMail is tightly integrated with Novell eDirectory. |
| | NetMail can also distribute e-mail and calendaring services across multiple servers. This increases performance while preventing critical processes from being interrupted by a system failure. |

| Objective | Summary |
| :--- | :--- |
| **2. Describe NetMail Components** | NetMail is composed of the following components:<ul><li>Internet Services Container</li><li>Messaging Server</li><li>Parent Objects</li><li>Templates</li><li>List Servers and Mailing Lists</li><li>NetMail Agents<ul><li>Address Book Agent</li><li>Alias Agent</li><li>AntiSpam Agent</li><li>AntiVirus Agent</li><li>AutoReply Agent</li><li>Calendar Agent</li><li>Connection Manager</li><li>IMAP Agent</li><li>List Server Agent</li><li>Modular Web Agent</li><li>NMAP Agent</li><li>POP Agent</li><li>Proxy Agent</li><li>SMTP Agent</li><li>WebAdmin</li></ul>During a default installation, NetMail files are copied to the /var/opt/novell/netmail and /opt/novell/netmail directories.</li></ul> |

| Objective | Summary |
| :--- | :--- |
| **3. Describe How NetMail Works** | When NetMail is installed, it expands the eDirectory schema to include NetMail-related objects and attributes.<br><br>Existing Directory objects, such as Container, User, and even Server objects, take on new NetMail attributes.<br><br>The core function of NetMail is message processing. Every message entering your messaging system must be processed by NetMail agents.<br><br>Depending on which agents you have running on your messaging system, the message might be checked against a system blacklist, forwarded to another email address, or filtered according to user-defined rules. |

| Objective | Summary |
| :--- | :--- |
| **4. Install NetMail** | NetMail can be configured in 2 ways:<br><ul><li><strong>Single-Server Messaging</strong></li><li><strong>Distributed-Server Messaging</strong></li></ul><br>When designing your NetMail system, you need to identify the following:<br><ul><li>Which servers will host NetMail agents?</li><li>Which agents will be located on a given server?</li><li>Which domains will be serviced by each messaging server?</li><li>Does your organization need fault tolerance and scalability by deploying the same agents on multiple servers?</li></ul><br>To install NetMail, you must meet the following system requirements:<br><ul><li>Ensure you're running 1 of the following:<ul><li>Red Hat Linux AS 2.1</li><li>Red Hat Linux ES 2.1</li><li>SuSE 8.0</li></ul></li><li>Ensure eDirectory 8.7.3 or later for Linux is installed.</li><li>Ensure your system CPU is at least a 750 MHz Pentium III or Athlon.</li><li>Ensure you have at least 512 MB of system RAM.</li></ul> |

| Objective | Summary |
| :--- | :--- |
| **4. Install NetMail (continued)** | - Make sure you have 20 MB of disk space free for installation.<br>- Each server hosting a NetMail service must have a replica.<br>- Make sure the eDirectory tree is synchronized and healthy.<br>- Make sure you have Admin rights to the eDirectory tree.<br>- Identify a name for the Messaging Server object.<br>- Identify your Internet domain DNS server IP address.<br>- Check for duplicate port assignments on your server. |
| **5. Configure and Use NetMail** | WebAdmin is the utility used to configure the NetMail system. It is a browser-based utility that is integrated into iManager.<br><br>To access WebAdmin directly, open a web browser and enter http://your_server_IP:8018 or https://your_server_IP:8020.<br><br>The NetMail system services all users in the containers configured in the Context property of the NMAP Agent.<br><br>By default, 2 templates ship with NetMail:<br>- WebAccess (Webacc.CTP)<br>- WebMail (WebMail.CTP) |

## SECTION 9: Unify NNLS Web Access with Virtual Office

In this section, you learn about the fundamentals of using Virtual Office to perform tasks such as creating and managing a team.

### Objectives

- 1. Describe Virtual Office
- 2. Install Virtual Office
- 3. Configure Virtual Office

### Introduction

Employees in the workplace today are becoming more mobile, often telecommuting, working at a branch office, or communicating from an Internet kiosk in a public place.

In this environment, employees need access to their email and work files. They might also need to access services such as printing, chat, team calendars, and team discussions.

Novell Virtual Office helps businesses solve these problems. Through an employee portal, it enables personal and group productivity functions along with Internet collaboration abilities, as shown in the following:

#### Figure 9-1

![](img/d63035f3fce0eaaf97203dde900affb7_225_0.png)

In this section, you learn how to install and configure Virtual Office to take advantage of NNLS products to make employees more productive while working remotely.

### Objective 1

### Describe Virtual Office

Virtual Office is a web access portal that allows remote users to collaborate and share information with a workgroup team.

The following is the default Virtual Office login page:

#### Figure 9-2

![](img/d63035f3fce0eaaf97203dde900affb7_226_0.png)

To describe Virtual Office, you need to understand the following:

- How Virtual Office Works
- Virtual Office Sample Scenarios

### How Virtual Office Works

Virtual Office optimizes the concept of self-service for users by letting them set up and manage many of their own networking, information-sharing, and data backup processes.

Virtual Office also lets users create their own functional teams, called Virtual Teams, for interactive real-time collaboration.

People who join a virtual team can access shared documents, discussion threads, bookmarks, and a team calendar. All members of the team have access to the team information and services.
