# Cluster Hooks Revisited

Now that we have a cluster up and running, it is time to expand upon those "hooks" within Tru64 UNIX that are used to more easily enable clustering. Our initial discussion started in chapter 6 and continued through chapter 9. In this chapter we will revisit the following topics:

+   - File System Hierarchy
+   - Member-Specific or Cluster-Common?
+   - Context Dependent Symbolic Link (CDSL)
+   - Hardware Management Databases
+   - Hardware Manager (hwmgr(8))
+   - Device Special File Manager (dsfmgr(8))
+   - Event Manager (EVM)
+   - Network Interface Failure Finder (NIFF)
+   - NetRAIN
+   - Link Aggregation (LAG)

| Revisited Coverage in Section | Original Coverage in Chapter |
|---|---|
| 12.1 | 6 |
| 12.1.1 | 6 |
| 12.2 | 6 |
| 12.3.1 | 7 |
| 12.3.2 | 7 |
| 12.3.3 | 7 |
| 12.4 | 8 |
| 12.5 | 9 |
| 12.6 | 9 |
| 12.7 | 9 |

# 12.1 File System Hierarchy Revisited

We begin our journey with the changes to the file system hierarchy now that the cluster has been created. The first change is the location of the file systems. In our standalone system, we had three file systems on two AdvFS domains:

+   - root_domain#root - the root (/) file system
+   - usr_domain#usr - the /usr file system
+   - usr_domain#var - the /var file system