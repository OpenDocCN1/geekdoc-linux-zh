When should you use a quorum disk? If you have a two-node cluster, a quorum disk is highly recommended. If your cluster is larger than two nodes, then it depends on how many nodes are in your cluster, although you should not configure a quorum disk in a cluster with an odd number of members. For more information on the Connection Manager and quorum within a cluster, please see Chapter 17.

During the initial creation of the cluster using the clu_create(8) command, you will be asked to provide a quorum disk. If your cluster will contain an even number of members and you plan to use a quorum disk, you can certainly provide the quorum disk when prompted. If you plan to operate the cluster as a single-member cluster for a while to "get the feel of the cluster," then we recommend that you refrain from creating the quorum disk during the initial creation of the cluster. After the second member is added to the cluster, the quorum disk can easily be added using the following command:

```
clu_quorum -d add <disk> <# of votes>.
```

If you find that you do not require a quorum disk and yet you plan to increase the number of members in your cluster at a much later date, then it would make sense to set aside a small disk on the shared bus that could be used as quorum disk. This disk can even be configured as a zero-vote quorum disk. See section 17.8.3 for further information.

# 10.1.4 Using the Cluster Preparation Worksheet and Checklist

In section 4.8, we created a Tru64 UNIX/TruCluster Server Planning Worksheet and Checklist. Using this Worksheet, you should be able to plan the implementation of your cluster in a very straightforward manner. Please use this as a guide upon which to build.

# 10.2 Installation of the TruCluster Server Software

Now that we have completed the planning and understand what it takes to build a cluster, let’s start by loading the TruCluster Server License PAK and installing the TruCluster Server software subsets. If you have already loaded the TruCluster Server License PAK onto your system, please jump ahead to section 10.2.2 on Installing the TruCluster Server Software.

# 10.2.1 Load the TruCluster Server License PAK

A quick and easy way to load a license PAK is to use lmsetup(8). We load the license PAK for TruCluster Server on the system that we will be installing and configuring the TruCluster Server software subsets.