
In this situation, the tree root partition is said to be a "parent" of the CLE partition because it resides higher in the tree hierarchy. The CLE partition is said to be a "child partition" of the root partition. Likewise, the CLE partition is the parent of the IF partition and the IF partition is a child of the CLE partition.

In eDirectory, parent/child relationships only go up or down one level, so the IF partition is not a child, or grandchild, of the tree root partition.

The first time I learned about partitioning back in the early 1990s, it scared me to death. I had some experience with hardware crashes, and the thought of taking a database and dividing it up among several servers made me cringe. What if one of the servers went down? The whole database could end up getting corrupted because a chunk of it would disappear.

Novell wisely accommodates for this reality. In addition to dividing up the eDirectory database into partitions, you can also place multiple copies of each partition on different servers. Each copy is called a *replica*.

eDirectory is designed such that changes made by an administrator (changing a password, for example) to one replica are quickly replicated to all the other replicas of that partition. All the servers that host a replica of a given partition are said to be members of the *replica ring*. Each replica has an attribute called **Replica**. This attribute contains a list of all the other servers in the replica ring for the given partition.

eDirectory uses this to make sure the data in all replicas of a given partition is always synchronized so that no matter what replica is used for a given network action, the data is always up to date.

For any given partition, four different types of replicas can be placed on servers in the tree:

- **Master replica**—The Master replica is created when a partition is defined. There can be only one Master replica per partition. As you can see in Figure 5.33, one partition was automatically created when you installed eDirectory that encompasses the whole tree. By default, your CLE1 server had a Master replica of the partition placed on it.

Because CLE1 is the only server in the tree, there is only one replica of the partition. All major partition operations, such as moves, merges, and creates, must be initiated from the Master replica.

Read/Write replica—Read/Write replicas are exact copies of the Master replica. Read/Write replicas can be used to authenticate to the tree and make changes to objects in the tree. The changes made are synchronized around to the other replicas of the partition, including the Master replica.

![](img/c7771e8540507f2b00c088c7a411b57b_232_0.png)

# FIGURE 5.33
Default partitioning and replication.

You can create as many Read/Write replicas of a partition as you wish. Novell recommends, however, that you don't create more than about 10 in order to keep the synchronization traffic on your network to a minimum.

Read/Write partitions can be configured as Filtered replicas. In a regular Read/Write partition, all data from the Master replica is synchronized. In a Filtered replica, you configure replication such that only specific data is replicated from the Master. For example, you may want a partition to only contain user objects. You can configure a filter on the replica that prevents anything, except for user objects, from being copied to the Filtered replica.

Read-Only replica—Read-Only replicas are just like Read/Write replicas, except for the fact that they can't be used to make changes to the objects in the tree. That's because they can only receive updates from the Master replica; they can't send them. Read-Only replicas aren't used very often. As with Read/Write replicas, you can create Filtered Read-Only replicas. They aren't all that useful, however—I've never actually seen anyone use one.

► **Subordinate Reference**—The Subordinate Reference (SR) is a tricky entity to understand. SRs aren’t really replicas. They contain no partition data. They are really more of a shortcut or a pointer that provides a reference to the location where the real data can be found.

SRs are automatically created. You can’t create them yourself. They are only created when a replica of a partition exists on a given server and that partition has one or more child partitions, but the server does not have a replica of those child partitions. The SR simply points to the servers where a real replica of the child partitions are placed.

The advantages to this partitioning and replication scheme are considerable. The partition aspect distributes the load among several servers, dramatically improving network performance. Replication ensures that multiple copies of each partition are placed on multiple servers in the network.

If one server goes down, the other servers holding replicas of the partition it contains automatically step in and service any network requests. The end user is able to keep working as though nothing happened.

Let’s practice working with basic eDirectory concepts in Lab Exercise 5.5.

## Lab Exercise 5.5: Managing eDirectory

In this lab, you're going to practice creating, deleting, and modifying eDirectory objects as well as working with eDirectory partitions. Complete the following:

1. Start **iManager** by opening a web browser (using the Mozilla icon on your desktop) and navigating to `https://your_server's_IP_address/nps/iManager.html`.
2. If prompted to accept a security certificate from your server, click **OK**.
3. In the **Username** field, enter **admin**.
4. In the **password** field, enter **novell** and then click **Login**.
5. Create a new Organizational Unit in the **CLE** container by completing the following steps:
    - a. Scroll down to **eDirectory Administration** and select **Create Object**.
    - b. In the **Available Object Classes** field, scroll down to and select **Organizational Unit** and then click **OK**.
    - c. In the **Organizational Unit name** field, enter **SLC**.
    - d. In the **Context** field, enter **CLE** and then click **OK**.
    - e. When prompted that the operation was successful, click **OK**.
    - f. Verify that the object was created by selecting **Modify Object**.
    - g. Next to the **Object Name** field, click the **Browse** button.
    - h. Select **Browse**.
    - i. Next to **CLE**, select the **blue down arrow**. You should see two containers listed: *IF* and *SLC*.
    - j. Select **Cancel**, **Cancel**.
6. Create a new user in the *IF* and *SLC* containers by completing the following steps:
    - a. Select **Create Object**.
    - b. In the **Available Object Classes** field, scroll down to and select **User** and then click **OK**.
    - c. Enter the following information in the respective fields:
        - Username: **CGrayson**
        - First Name: **Christopher**
        - Last Name: **Grayson**
        - Context: IF.CLE
        - Password: novell
        - Title: **Director**
        - Location: **Idaho Falls, Idaho Office**
        - Department: **Training**
        - Telephone: 555-555-5555
        - Fax Number: 555-555-4444
        - E-mail Address: cgrayson@cle.com
    - d. Select **OK**.
    - e. When prompted to convert the user to a LUM object, click **Cancel**.
    - f. Repeat this process to create the following user:
        - Username: **DCoughanour**
        - First Name: **Dave**
        - Last Name: **Coughanour**
        - Context: SLC.CLE
        - Password: novell
        - Title: **President**
        - Location: **Salt Lake City, Utah Office**
        - Department: **Executive Management**
        - Telephone: 555-555-5555
        - Fax Number: 555-555-4444
        - E-mail Address: dcoughanour@cle.com
7. Give CGrayson management rights to the IF container by completing the following steps:
    - a. In iManager, scroll down to **Rights** and select **Modify Trustees**.
    - b. In the **Object Name** field, enter IF.CLE and then click **OK**.
    - c. Select **Add Trustee**.
