The modular nature of NetMail provides you with a great deal of flexibility in how it is deployed. The first topic we need to cover here is how to plan your NetMail deployment.

# # Planning Your NetMail Deployment

The way you deploy NetMail is heavily dependent on the load you anticipate it to handle. If your NetMail system will be servicing tens of thousands of users, you may want to consider a distributed system.

According to Novell, a single Linux server running NetMail can handle up to 30,000 users and 1.1 million messages a day. This probably works great in the lab, but in a production environment, you should probably scale that number back to around 10,000 users.

Both of these numbers assume that you aren’t running much else on the server, such as iFolder or iPrint. If you’re running multiple services on the single server along with NetMail, you should reduce the maximum number of supported users even further.

Even at that, it should be noted that a single NetMail server supports a tremendous number of users when compared to other competing enterprise email solutions. This serves as a strong testament to the scalability of both the Linux operating system and Novell’s NetMail service. Let’s look at how a single-server system is implemented.

# ## Single-Server Deployment

In a single-server deployment, all the NetMail components are installed on the same server, as shown in Figure 10.25.

![](bbox=[0.19, 0.72, 0.65, 0.96])