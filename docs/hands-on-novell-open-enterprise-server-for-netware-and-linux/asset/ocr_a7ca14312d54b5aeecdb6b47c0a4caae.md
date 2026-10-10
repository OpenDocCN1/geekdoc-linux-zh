![](bbox=[0.1, 0.05, 0.45, 0.16])

Figure 10-5 The completion message for iFolder installation

# Configuring iFolder

After installing the iFolder software on the NetWare 6.5 OES server, you need to use the iFolder Management utility to configure the iFolder server and enable user accounts. The iFolder management utility is accessed from the URL https://IPaddress/iFolderServer/Admin (substituting the iFolder server's IP address or DNS name for IPaddress). The iFolder Management utility divides iFolder administrative tasks into four major categories, as shown in Figure 10-6.

![](bbox=[0.1, 0.33, 0.55, 0.6])

Figure 10-6 iFolder management options window

Before performing these administrative tasks, you need to log in to the iFolder server with the Admin user name and password you specified during iFolder installation. In the following sections, you learn how to use the iFolder management tasks to configure the iFolder environment.

# Configure Global Settings

Under the Global Settings heading are the five links shown in Figure 10-7. The General Information window displays basic information about the iFolder server, including the DNS name or IP address, the port being used, the default context, and the vendor version. This information is for reference only and cannot be changed.

Clicking the Global Policies link displays options for Client Policies and Server Policies. Administrators can use the Client Policies window shown in Figure 10-8 to set parameters that affect new and existing users. Certain parameters, such as Encryption, Recover Pass Phrase, and iFolder Location, affect only new iFolder user accounts. Automatic synchronization settings enable administrators to set how often the iFolder client synchronizes its data with the server. The iFolder location, set only on new user accounts, identifies the path where iFolder data is stored on the client computer. For most purposes, these default settings don't need to be modified.