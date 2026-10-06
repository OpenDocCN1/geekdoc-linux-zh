# CHAPTER 25 Distributed File Systems (DFS) 645

![](bbox=[0.179, 0.126, 0.781, 0.439])

**Figure 25-1** Traditional network file server and LAN clients

In Figure 25-2, things are switched around a little: We've added more client systems. In addition to the elements and conditions shown in Figure 25-1, our new scenario has the following elements:

+   * A bunch of new client systems—client-G, client-H, client-I, and client-J—that need access to MASSIVE_DATA on server-A.

+   * The new clients, are not directly connected to the LAN as server-A. Instead they are connected over a WAN (Internet).

+   * The new clients are located in physically and geographically different locations.

Obviously, nothing has much changed as far as server-A is concerned—a bunch of new clients requiring access to MASSIVE_DATA.

However, a problem is created by the new requirements: even though server-A may still be up to the task of making its file system available to the new additional clients, the intervening network between the server and the new clients might not be up to