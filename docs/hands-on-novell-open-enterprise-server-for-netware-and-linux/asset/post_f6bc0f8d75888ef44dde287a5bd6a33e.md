
## PLANNING THE eDIRECTORY TREE STRUCTURE

users to log in by simply typing the common name for their user accounts. If users need to log in outside their current context, they can by specifying the distinguished names for their user accounts. For example, Eric wants to log in from another computer that has its current context set to the Engineering OU. To log in, he could type his distinguished name—E.Kenton.IT.UAS—in the Username text box, or click the Advanced button to set the current context to the IT container. In “Working with Novell Client” later in this chapter, you learn how to customize Novell Client to set your computer’s current context to a specific location in the eDirectory tree.

If your client computer’s current context is set to one of the containers specified in the distinguished name, you can save keystrokes by using a relative name. A *relative distinguished name* starts with the client’s current context and is specified by omitting the leading period. For example, if the client’s current context is set to the UAS container, Eric could log in by entering a relative name or distinguished name in the Username text box:

- E.Kenton.IT (relative distinguished name—note that the name does *not* start with a period)
- .E.Kenton.IT.UAS (distinguished name—note that the name starts with a period)

Another way to specify a relative name is by ending the name with a period, which causes the eDirectory system to move the current context up one level before searching for the object. For example, if the current context is .Engineering.UAS, Eric could log in to the IT container by entering E.Kenton.IT. in the Username text box.

One of the first tasks in setting up eDirectory is to design the eDirectory tree structure for the organization. A first step is analyzing the organization’s workflow and resource-sharing needs to determine what containers are needed. Although this task can be complex for large corporate networks, it can be quite simple for small single-server networks. Eric did this for the UAS eDirectory tree by grouping the objects into containers based on resource sharing. When grouping objects, you should keep the design as simple as possible to reduce the number of containers that are needed. A basic guideline is to avoid creating containers for fewer than 10 objects. An exception to this guideline is when user objects are located in separate geographical areas with their own server and independent resources. Grouping objects in different geographic areas into separate containers makes it possible to partition the eDirectory database for better efficiency, as described in “Implementing eDirectory Partitions and Replicas” later in this chapter. For example, Universal AeroSpace has a small subsidiary called AeroDyn that needs only five user accounts. Because the AeroDyn facility is in another city, Eric has decided to create a separate OU for it, even though it has fewer than 10 users.

The next step is to design the eDirectory tree structure for the organization by placing the containers in a hierarchical tree structure. Novell recommends that each tree have only one Organization container for objects shared by the entire organization. In a simple tree design, the Organization container might be the only container object needed. Although this design would work for a small company, most organizations need to divide network objects into OU containers for departments and workgroups. When designing your eDirectory tree hierarchy, you should strive to keep the number of OU within OUs to a minimum. Placing OUs with other OUs creates long distinguished object names and can make finding objects in the tree more difficult. However, sometimes this method can be useful for mirroring departmental structures, as in the UAS eDirectory tree used throughout this book.

Figure 4-13 shows the tree design Eric developed for UAS. Because the Engineering Department monitors many of the manufacturing processes, Eric decided to place the container for Manufacturing in the Engineering OU. Both the Universal AeroSpace and AeroDyn divisions have manufacturing facilities in different cities, so Eric designed separate containers for AeroDynMfg and UasMfg in the Mfg OU. Eric plans for the Business OU to include leaf objects for the Business Division, including the Desktop Publishing, Accounting, and Marketing departments.

![](img/840007e8f98ea6653e5877e945c27dc6_158_0.png)

Figure 4-13 A sample UAS eDirectory tree design

Because users in each department have different needs in terms of resources and access rights, separating them makes it easier to assign user access rights, partition the database, and manage the network in the future. Although the Sales and Desktop Publishing departments could also be separated from the Business OU, the few objects in those OUs wouldn't justify the complexity of the additional network directory design. In addition, because of their physical proximity, users in these departments often share access to network printers and other resources as compared to, the Manufacturing Department, which has network objects spread between the AeroDyn and UAS facilities in two different cities.

## Creating eDirectory Objects

To implement and maintain the eDirectory tree, you need to become familiar with Novell's management utilities. In previous NetWare versions, implementing and managing the eDirectory tree required running the Console One or NetWare Administrator utility on a computer with Novell Client installed. In NetWare 6.0, Novell introduced a new network management tool called iManager. Like Remote Manager, the iManager utility is designed to run from the Web browser of any desktop OS, enabling the administrator to perform network management tasks from any location. In this chapter, you work with iManager to set up containers and leaf objects for the UAS eDirectory tree. In Chapter 5, you learn how to use Console One and NetWare Administrator in the Windows environment to manage the eDirectory tree.

## Using the iManager Utility

As we learned in Chapter 1, one of Novell's objectives in the OneNet strategy is to make it easier to manage and maintain the organization's network from any computer, regardless of the type of computer you're working on or the network system it's attached to. In Chapters 2 and 3, you learned how to use Remote Manager to manage the NetWare 6.5 server via a Web browser. In addition to Remote Manager, NetWare 6.5 ships with the iManager 2.5 utility, which makes managing and maintaining eDirectory possible from a Web browser. To run iManager, start your Web browser and then enter the iManager URL of "/nps/iManager.html". For example, if your server is assigned the IP address 172.20.0.65, you enter "https://172.20.0.65/nps/iManager.html". The "https" tells the browser to use a secure connection with Secure Sockets Layer (SSL), and "/nps/iManager.html" directs the NetWare Web server to open the Novell iManager Login window shown in Figure 4-14.

138   Chapter 4   Novell eDirectory Services

![](img/840007e8f98ea6653e5877e945c27dc6_159_0.png)

Figure 4-14 The Novell iManager Login window

Before the iManager Login window is displayed, you might see a security alert message informing you that you're about to view pages over a secure connection. Click OK to continue. You might see another security alert message informing you that the security certificate was issued by a company you have not chosen to trust. Security certificates accompany the key sent from the server to the client to encrypt data before sending it over the Internet. Certificates are described in more detail in Chapter 11.

After you log in successfully, iManager displays the main window shown in Figure 4-15.

![](img/840007e8f98ea6653e5877e945c27dc6_159_1.png)

Figure 4-15 The Novell iManager main window

In Activity 4-1, you use iManager to set up the eDirectory structure shown previously in Figure 4-13. After creating the structure, you use iManager to create an alias object in Activity 4-2 and user accounts in Activity 4-3.
