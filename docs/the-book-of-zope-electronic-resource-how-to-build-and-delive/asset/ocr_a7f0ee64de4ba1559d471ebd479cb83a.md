# 4.3.11 The tree Tag

The tree tag is used to survey Zone objects in their hierarchy and present them as a tree structure with collapsible branches and leaves. Thus, you can create a tree structure like the one used in the left-hand frame of the management interface. In the example in Figure 4-8, a folder named Folder1 contains several:

| Type Name | Size | Last Modified |
|---|---|--|
| Subfolder1 | | 2001-05-27 22:36 |
| Subfolder2 | | 2001-05-28 02:17 |
| acl_users (User Folder) | | 2001-05-27 22:06 |
| dmtl_document2 | 1 Kb | 2001-05-27 02:18 |
| dmtl_method1 | 1 Kb | 2001-05-27 22:19 |
| dmtl_method2 | 1 Kb | 2001-05-27 22:19 |
| index_html | 1 Kb | 2001-05-27 22:06 |

Figure 4-8: The objects in Folder1

To create a simple tree structure, use the tree tag in a DTML method located in Folder1:

```
<dmtl-tree>
<dmtl-var name=" id">
</dmtl-tree>
```

The tree appears in the third tier view as shown in Figure 4-9.

![](bbox=[0.218, 0.523, 0.415, 0.658])

Figure 4-9: A simple tree structure view

The tree in Figure 4-9 displays onlyish objects located in the current folder and is visually less attractive than the one used by the management interface. The tree tag itself is very complex and accepts a wide variety of attributes that can be used to format a tree view. For example, to start a tree from a location other than the one the DTML method is located in, you must specify the name of the object from which the tree should start, like so:

```
<dmtl-tree name="Subfolder1">
```

The branches and branches_expr attributes are set as standard for the method tpValues. The method with which all objects and subobjects is found called objectValues. These methods are defined for you in folderish objects.