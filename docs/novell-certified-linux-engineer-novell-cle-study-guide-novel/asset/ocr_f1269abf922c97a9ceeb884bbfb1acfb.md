![](bbox=[0.18, 0.09, 0.66, 0.29])

# FIGURE 5.28
eDirectory tree.

Figure 5.28 depicts the eDirectory tree you installed in an earlier lab exercise. Notice that the name of the eDirectory tree is **CLE-TREE**. The tree is the topmost container in the hierarchy. Within the tree is a container object called **CLE**. Inside of CLE is another container object named **IF**. Within IF are several leaf objects, including the **admin user** object and the **RCD Group** object you created.

This brings up an issue that I’ve observed over the years. Because many network administrators who move to eDirectory come from a Windows NT, NetWare bindery, or Linux/Unix passwd file background, they make a key error when installing eDirectory.

Generally speaking, an organization should have *one* eDirectory tree. Because of their previous experience with these other flat-file databases, however, administrators install each eDirectory server in their organization into its own tree.

A Novell technical support engineer once related to me an instance when she received a support call from an individual who had made this very mistake. After asking several exploratory questions trying to discern the customer’s problem, she discovered that the administrator had more than 50 eDirectory servers in his network and had installed each one into its own tree.

If you do this, you’re stuck with a system that isn’t much better than the flat-file database systems you migrated from. Each tree operates completely independent of the other trees in your network. Remember that you can (and should) install all your servers into the same eDirectory tree.

You’ve probably noticed in Figure 5.28 that the icons representing the CLE and the IF containers are different. That’s because they represent different types of container objects. In eDirectory, there are three types of containers within the tree container: