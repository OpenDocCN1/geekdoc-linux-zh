
I always found it funny that the members of my team (myself included) would use email almost exclusively to communicate, even though we all sat within 30 feet of each other. We could have just as easily poked our heads over the cubicle walls and communicated verbally. This dynamic has been repeated in corporations and other organizations around the world.

To further demonstrate this dependence, imagine what would happen in your organization if your email server were to go down. I've also experienced this scenario on occasion. When the email system goes down, productivity in the organization slows to a crawl.

With this in mind, NNLS includes a powerful email solution for your implementation: NetMail. If you've worked with Linux previously, you know that many email solutions are already available for this platform. If you're running SUSE, the postfix mail service is automatically installed. If you're running most other distributions, your system is probably running a version of sendmail.

In and of themselves, these two services are pretty basic. If you search Open Source websites, such as Sourceforge.net, you can find numerous add-ons, such as POP3, SMTP, and web interface support, to these services that turn them into full-service email solutions.

If you want an email solution with a little more muscle, you could also implement SUSE's Openexchange email server. Openexchange is a very powerful email solution (also available from Novell through its acquisition of SUSE). With all these email solutions available, why should you consider implementing the NetMail component of NNLS?

The answer relates to one of NetMail's key benefits: NetMail is fully integrated with eDirectory. Other than Novell's new GroupWise for Linux release, no other email package boasts the level of eDirectory integration provided by NetMail.

> **NOTE** Due to the way GroupWise works with eDirectory, many would argue that NetMail provides a higher level of eDirectory integration than GroupWise. We're not going to get into that argument in this book. The NetMail-versus-GroupWise tensions within the Novell community can run very high.

In Chapter 5, “NNLS Installation and Administration,” I stated that eDirectory is the backbone of NNLS. By now, you should fully understand this statement. Every product you have implemented so far, from eGuide to iPrint, relies on eDirectory as a data store and as an authentication system. NetMail is no different. It leverages eDirectory to store its server configuration settings as well as to authenticate users.

If you were to implement a different email package, you would have to maintain a separate set of user accounts. In a very small company, this may not pose a serious problem. But in medium-to-large organizations, this represents a tremendous (and expensive) workload for the network administrator. By implementing NetMail, every user in your tree can have an email account. When new users are added to the tree, they automatically have an email account.

Let's review some of the features of NetMail.

## NetMail Features and Benefits

In addition to eDirectory integration, NetMail provides the following features and benefits:

- NetMail is very easy to deploy.
- NetMail is less expensive to maintain than other Linux email products.
- Using standards-based protocols, including POP3 and IMAP, the NetMail server is compatible with all email client software, including Novell's GroupWise client and Microsoft's Outlook client.
- NetMail is highly scalable. A single Linux server can support thousands of email users. Novell has even tested NetMail successfully with 30,000 email users on a single Linux server!
- NetMail is modular. Different NetMail components can be distributed among Linux servers in your network. This even further enhances NetMail's scalability. Modules can also be distributed redundantly, providing a degree of fault tolerance in the event of a server failure.
- NetMail supports multiple processors.
- NetMail supports Secure Sockets Layer, Transport Layer Security, and Secure MIME protocols to protect data.
- NetMail provides a web-based user interface, allowing full-featured access without email client software.
- NetMail provides a full collaboration solution by providing email, calendaring, and scheduling services.

As you implement NetMail in this chapter's lab exercise, you will come to understand just how powerful this NNLS component really is. Before we get into the installation and configuration of NetMail, however, you need to understand the various components that comprise the product.

# NetMail Components

As mentioned previously, NetMail is a highly modular product. This modularity allows you to distribute your implementation among several Linux servers, which can make your system very fast.

It also allows you to customize your deployment to meet your organization's requirements. This is done by only deploying the NetMail components that you need. This further increases NetMail's scalability and speed. Alternatively, you can also install all your required NetMail components on the same Linux server. NetMail components are referred to as *agents*. Let's discuss the role and function of each agent.

## NetMail Agents

Each NetMail agent is represented by an object in the eDirectory tree. This is shown in Figure 10.1.

**FIGURE 10.1**
NetMail agents.

![](img/c7771e8540507f2b00c088c7a411b57b_453_0.png)

Each agent provides a particular service to the NetMail system. One may provide POP3 support, one may provide IMAP support, and another may provide an address book function. Functioning together, these agents make up the entire NetMail system. The agents provided by NetMail include the following:

- **The Address Book Agent**—This agent allows LDAP-compliant email clients to populate their address books with user information from your eDirectory tree. The Address Book Agent uses IP port 52389. The Configuration attributes of the Address Book Agent are shown in Figure 10.2.

**FIGURE 10.2**
Address Book Agent object properties.

![](img/c7771e8540507f2b00c088c7a411b57b_454_0.png)

- **The Alias Agent**—The Alias Agent is used to automatically generate email addresses for users. The email addresses generated are referred to as *user aliases*. You can generate user aliases using various combinations of the user objects' given name and surname attributes. For example, you could configure a user alias to be formatted as *givenname.surname@your_domain*, *givenname_surname@your_domain*, or *givenname_first_letter+surname@your_domain*.

> Don't confuse these aliases with *alias objects* in the eDirectory tree (as discussed in Chapter 5). The email aliases generated by the Alias Agent are stored in memory, not in the eDirectory tree.

This value is used to automatically populate the Internet Email Address property of user objects in your tree.

- **The AntiSpam Agent**—The AntiSpam Agent in NetMail allows you to configure spam filters for your implementation. The filtering capabilities are relatively basic, but they can be very effective. The AntiSpam Agent allows you to build a list of filtered domains and/or email addresses from which your NetMail system will refuse to accept email messages. The attributes of the AntiSpam Agent object are shown in Figure 10.3.

- **The AntiVirus Agent**—The AntiVirus Agent allows you to integrate third-party antivirus programs with your NetMail system. The AntiVirus Agent will delete any infected messages from the system. It can also be configured to return an infected message back to the sender or just send a notification that an infected message was received.

**FIGURE 10.3**
AntiSpam Agent object properties.

![](img/c7771e8540507f2b00c088c7a411b57b_455_0.png)

The AntiVirus Agent supports McAfee NetShield, CA InoculateIT, Symantec CarrierScan, and Command Antivirus. To use these products, you must install and configure them *prior* to configuring the AntiVirus Agent.

- **The AutoReply Agent**—The AutoReply Agent allows users to configure autoresponses for their email accounts. Users can configure a message to be automatically sent to senders. They can also configure received messages to be forwarded to a different email address.

- **The Calendar Agent**—The Calendar Agent in NetMail allows users to schedule appointments and invite other users to attend. When this is done, the invitees are sent an appointment and given the opportunity to accept or decline the invitation.

The NetMail system keeps track of users who have accepted and who have declined, allowing the user who scheduled the appointment to identify who will be attending.

This agent is optional if you are using email client software that supports its own calendaring system (such as Outlook XP). If so, you can let the clients manage calendaring tasks by not implementing the
