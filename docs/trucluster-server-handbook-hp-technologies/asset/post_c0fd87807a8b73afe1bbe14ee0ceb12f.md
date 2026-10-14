
`clu_migrate_configure`

The `clu_migrate_configure` script configures the storage and file systems on the V5.X cluster using the data saved by `clu_migrate_save`. Of the four scripts, this is the only one that runs on the V5.X cluster. This is used in option 2 or option 3.

Note: Use "`clu_migrate_configure -x`" to see what `clu_migrate_configure` would do without actually carrying out any of the instructions.

For more details about the `clu_migrate_*` scripts, refer to Chapter 8 of the *TruCluster Server Cluster Installation Manual*.

## 26.3 Migration Options

How then do you migrate a V1.5/6 cluster to V5.X when you can’t perform a rolling upgrade and you can’t have the V5.X cluster connected to the V1.5/6 cluster (in any way except possibly on a LAN)? You have three options from which to choose. These options are usually thought of as a trade-off between downtime and expense.

- Option 1:
  Create a separate cluster consisting of new systems and storage. Once this cluster is built and tested, migrate the functionality from the V1.5/6 cluster to this new V5.X cluster. The problem is that few people have the luxury of obtaining this additional hardware.

- Option 2:
  Create a separate, perhaps limited cluster with new systems and at least enough storage to establish the cluster and test your applications. Once the new cluster is fully configured and tested, physically connect the old storage from the V1.5/6 cluster to the new cluster. This option is slightly less expensive than option 1 but still requires additional hardware.

- Option 3:
  Upgrade the existing V1.5/6 cluster using its hardware and storage. Remove and disconnect one member from the V1.5/6 cluster, install and configure a standalone Tru64 UNIX V5.X system, shut down the remaining systems in the V1.5/6 cluster, connect the V1.5/6’s storage to the standalone V5.X system, configure the storage, create a single-member cluster, and then add the other systems to the new cluster. This option requires the least amount of additional hardware (perhaps some additional disks, HBAs, and LAN interconnect cards (if using LAN interconnects for the cluster interconnect)).

## 26.4 Migration Example

Let’s run through our "option 3" example. We will mostly use existing hardware, configure and test the version 5.X cluster while a reduced version 4.X cluster continues our live production, then complete the migration with a minimum of downtime. If there is a problem with the V1 applications or CAA resources, you will see how to return to the full version 4.X cluster.

### 26.4.1 Planning

Plan. We cannot emphasize enough the importance of planning your migration and your cluster layout. If you skip this step, you may be forced to rebuild the cluster in the not too distant future. Part of your planning process should include reading the TruCluster manuals. The TruCluster Server Cluster Technical Overview is a small manual, which you should read cover to cover because it will ground you in the TruCluster Server components and technology. Another crucial part of planning is determining which layered products you will need to upgrade. Don’t gloss over this point because some of your layered products that run on V5.X could differ from your current version and therefore require learning an updated product.

### 26.4.2 Check Your Existing Hardware for Compatibility

After you’ve planned how the cluster will be laid out and migrated, you are ready to begin the process. Install the TCRMIGRATE5X5 subset and run clu_migrate_save (to build the data that will automate part of the migration). Also run “sys_check –escalate” on each member (both as a precautionary measure – you want this data in case you have to repeat part of the V1.5/6 infrastructure – and so you can see what hardware you have on the cluster). As a result of planning and reviewing the “sys_check –escalate” data, purchase any hardware necessary for the new cluster. This would also be a good time to consider converting any UFS file systems to AdvFS. If you convert the file system(s) now, you won’t have to repeat the task should the migration fail to complete for some reason. Figure 26-1 shows our V1.5/6 cluster starting point.

Note: By converting to AdvFS at this state, you will be taking the old AdvFS on-disk structure forward. You should, at a later time, convert to the new structure by creating a new file domain and restoring the data to that domain.

### 26.4.3 Divide and Conquer

Pick a member to remove from the V1.5/6 cluster (this will be our V5.X cluster beachhead). Add any of the identified required hardware to that system. Also update the firmware and install Tru64 UNIX V5.X on the removed system as seen in Figure 26-2. Notice that neither the storage nor the cluster interconnect is shared at this point. Remember, we recommend a fresh install of V5.X, not an installupdate to V5.X, because there are many major changes in the OS since V4.X (AdvFS, LSM, and clustering, just to name a few).

### 26.4.4 Create a TruCluster Server Cluster

Install TruCluster Server on your newly installed V5.X system. This is a good time to apply the latest patch kit. (Simply installing the TruCluster subsets does not create a cluster.) Also, you should partition your disks for the cluster-common file systems (cluster_root, cluster_usr, and cluster_var). Now run clu_create to create a single-member cluster. Your new “split” cluster should look something like Figure 26-3. Again, these are two completely separate one-member clusters.
