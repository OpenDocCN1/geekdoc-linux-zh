local to the server. To get around this, many Linux administrators employ the NIS+ service, which synchronizes user accounts among Linux servers. eDirectory changes all that. With this service, all the servers on your network are installed into the eDirectory tree. User accounts are also created in the tree. Users have one single account that gives them access to network resources.

Instead of logging in to a specific server, users authenticate to the eDirectory tree. From there, they can access any network data or resource they have been granted access to, regardless of what server is hosting the resource.

In addition, applications can be easily written that access directory information. As you will see later in this book, all NNLS components do just that. They use eDirectory information to control access, display information, and provide services.

eDirectory fills the following primary roles:

+   - Storing network data in a central repository
+   - Organizing network data into a logical structure
+   - Providing standardized methods for accessing network data
+   - Controlling access to network data
+   - Securing network data

Let’s now discuss how eDirectory works.

# ## How eDirectory Works

When discussing how eDirectory works, we’re going to stay at the conceptual level. Recently, I had the opportunity to spend time with the software developers at Novell who actually wrote the eDirectory code, learning about the inner workings of the product. My head was swimming after only a few minutes (and I had considered myself an eDirectory veteran!). We will discuss the following topics:

+   - The structure of the eDirectory tree
+   - How eDirectory naming conventions work
+   - How eDirectory rights work
+   - How eDirectory embraces the Lightweight Directory Access Protocol (LDAP) standard