In addition, the `xnwdstrustees` utility can be used to make rights assignments changes and to add new trustees.

# VIEWING ATTRIBUTES OF AN NDS OBJECT

The `nwdattrs` utility enables you to view the NDS attributes for an object class by specifying an existing object. The following syntax is used:

```
nwdattrs -o <PATH>
```

The `<PATH>` option is the NetWare automounted path of an NDS object.

You can view the attributes for an Organization object by pointing to the O=CALDERA container. To accomplish this, issue the following command:

```
nwdattrs -o /NetWare/NDS/NW-TREE/CALDERA
```

The results of this query are shown in Figure 28.6.

**Figure 28.6**  
NDS attributes for an Organization object.

![](bbox=[0.205, 0.386, 0.739, 0.67])

# VIEWING VALUES FOR NDS OBJECT ATTRIBUTES

The `nwdvalues` utility can be used to display the values of NDS object attributes for a specified object. The following syntax is used (Table 28.15 shows the possible command-line options for `nwdvalues`):

```
nwdvalues [OPTIONS]
```

**Table 28.15 — Command-Line Options for `nwdvalues`**

| Options | Description |
|---|---|
| `-o <PATH>` | NetWare automounted path for NDS object being queried |
| `-a <ATTRIBUTE>` | Attribute of object being queried |
| `-h` | Displays command help |