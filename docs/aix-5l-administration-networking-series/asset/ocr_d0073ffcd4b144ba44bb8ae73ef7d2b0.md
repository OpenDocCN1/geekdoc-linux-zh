**mkdec1ient**, but select dfs_cl for “CLIENTS to configure” if the base DCE clients are already running on this machine. You may select both all_cl and dfa_cl on remote DFS client machines that do not have DCE clients configured. Use the following command and select Full when prompted, then refer to Figure 15-3 and take all the defaults not highlighted in the following SMITTY panel:

```
# smitty mkdec1ient                     FastPath to Full DCE/DFS Client Configuration
```

You should now be able to see the DFS shared root with the following df command:

```
# df /...
Filesystem 512-block  Free %Used Iused %Iused Mounted on
DFS        18000000 18000000   0%      0    0% /...
```

# Creating and Exporting Aggregates

Create an aggregate logical volume to hold the LFS files. Use the **mklv** command to create a logical volume with type set to lfs in the target volume group. This lls type

![](bbox=[0.1, 0.52, 0.83, 0.88])

Figure 15-3. SMITTY Full DCE/DFS Client Configuration (smitty mkdec1ient)