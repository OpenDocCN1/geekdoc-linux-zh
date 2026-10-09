```
lfs01 (/dev/lvfs01): id=1 (LFS)

# fts lfs -fileset root.dfs

root.dfs 0,1 RW LFS       states 0x10010005 On-line
rs250.mcgraw-hill.com, aggregate lfs01 (ID 1)
Parent 0,0   Clone 0,2   Backup 0,3
llBack 0,0   llFwd 0,0    Version 0,1
Infinite alloc limit;    9 K alloc usage
5000 K quota limit;       9 K quota usage
Creation Mon May 27 16:50:48 2002
Last Update Mon May 27 16:50:48 2002
ll reads, 0 writes in 36779 seconds since Mon May 27 16:50:48 2002
0.000299084 reads per second; 0 writes per second.
```

```
root.dfs
    readWrite   ID 0,1 valid
    readOnly    ID 0,2 invalid
    backup      ID 0,3 invalid
number of sites: 1
    server    flags   aggr   siteAge  principal  owner
rs250.mcgraw-hill.com  RW  lfs01  0:00:00  hosts/rs250  <nil>
```

```
# dfsexport
Aggregate  Device  Name   Type  Aggr  ID  Non-LFS  fileset ID
/dev/lvfs01    lfs01   lfs    1
```

# OPERATION AND ADMINISTRATION

We have already covered a number of the commands used to administer DFS. Each of the DFS commands supports enough options and parameters that the permutations and combinations are well beyond what can be covered in a single chapter. Table 15-3 lists the base commands with a short description and the following command-line help syntax will provide brief listings of available options for most of those commands.

```
# Command&Name help [option]  <——Display command help
# CommandName option -help  <——Handy alternative help
```