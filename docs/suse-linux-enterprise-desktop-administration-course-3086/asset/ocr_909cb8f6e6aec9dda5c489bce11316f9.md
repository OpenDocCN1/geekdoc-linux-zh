Notice that the Owner is Geeko Chameleon.

However, the Owner, Group, and Others only have the Read and Execute permissions because the folder was copied from a DVD.

+   f. For the Owner, select (check) the Write permission; then select Close.
+   g. Right-click an empty area on the SLED 10 desktop; then select Open Terminal.
+   h. Switch to the root user by entering su - with a password of n0v311.
+   i. Change to the iFolder_Client folder by entering
+   j. Display the contents of the iFolder_Client folder by entering ls -l.
+   Notice the three rpm files: one for the Novell iFolder client, one for the Nautilus Web browser, and one for Simias.
+   k. Install all three rpms at the same time by entering
+   l. Close the terminal window by entering exit twice.

```
cd /home/geeko/Desktop/iFolder_Client
```

```
rpm -ivh *
```

The Novell iFolder client begins installing.

When the installation is complete, you are returned to the command prompt.

# 2. Configure a Novell iFolder account on SUSE Linux Enterprise Desktop 10:

+   a. From the DAxx SLED 10 workstation desktop, select Computer > More Applications.
+   b. From the Application Browser dialog (on the right), select the iFolder 3 icon. After a few moments, an iFolder Account Assistant dialog appears, as shown in Figure 13-40, to help you create a Novell iFolder account.

![](bbox=[0.17, 0.6, 0.68, 0.9])

Figure 13-40