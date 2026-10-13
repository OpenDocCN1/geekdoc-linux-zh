
## Assigning NetWare Filesystem Rights to Bindery Objects

`nwboaddtrust` and `xnwbotrustees` are the two utilities available to make NetWare bindery objects trustees of directories or files, and to make rights assignments. The following syntax is used (Table 28.20 shows the possible command-line options for `nwboaddtrust`; Table 28.21 shows the possible command-line options for `xnwbotrustees`):

```
nwboaddtrust [OPTIONS]

xnwbotrustees [OPTIONS]
```

**Table 28.20 — Command-Line Options for nwboaddtrust**

| Options | Description |
|---|---|
| `-o <OBJECT>` | Object being made a trustee and receiving rights |
| `-p <PATH>` | Directory or file to which the trustee assignment is being added |
| `-r [RWMCEFA]` | Rights to assign to the new trustee—the possible rights are as follows:<br>R = Read<br>W = Write<br>C = Create (only applicable for directories)<br>E = Erase<br>M = Modify<br>F = File scan<br>A = Access control |
| `-h` | Displays command help |

To make the user `jsmith` in the NetWare bindery for server `OPENLINUX` a trustee of the `SYS:groups\acctg` directory, and to assign read, write, and create rights, use the following command:

```
nwboaddtrust -o /NetWare/bindery/OPENLINUX/objects/jsmith -r [RWC] -p /NetWare/bindery/OPENLINUX/volumes/SYS/groups/acctg
```

If the user `jsmith` is already a trustee of the `acctg` directory, his rights will be overridden by the new assignment.

**Table 28.21 — Command-Line Options for xnwbotrustees**

| Options | Description |
|---|---|
| `-p <PATH>` | Directory or file to which the trustee assignment is being added |
| `-h` | Displays command help |

The `xnwbotrustees` utility gives you a graphical interface for adding trustees and making rights assignments to files and directories.

To make the user `jsmith` in the `OPENLINUX` server NetWare bindery a trustee of the `SYS:groups\acctg` directory, and to assign read, write, and create rights, use the following command:

```
xnwbotrustees -p /NetWare/bindery/OPENLINUX/volumes/SYS/groups/acctg
```

The command brings up the graphical interface shown in Figure 28.7.

**Figure 28.7**  
The nwbotrustees utility window.

![](img/c741b1b6b6eccaba2ad43454c979a7f8_554_0.png)

After the window opens, you need to perform the following steps to accomplish the desired results:

1. Click **Add Trustee** in the Directory Trustees window.
2. Type the username in the **New Trustee** field.
3. Choose the rights that you want to give `jsmith` by clicking the appropriate check boxes (treat the **Change** option as the Create Right).
4. Click the **Add Rights** button.

After you have performed these steps, the same command that brought up the graphical interface can be used to modify or remove the rights assigned to `jsmith`.

## Viewing NetWare Filesystem Trustees Assignments and Rights

The `nwboshowtrust` utility can be used in one of two ways. You can use it to show directories or files on a server of which the specified object is a trustee, or you can use it to list all trustees of a specific directory or file. The following syntax is used (Table 28.22 shows the possible command-line options for the `nwboshowtrust` utility):

```
nwboshowtrust [OPTIONS]
```

**Table 28.22 — Command-Line Options for nwboshowtrust**

| Options | Description |
|---|---|
| `-o <OBJECT PATH>` | Specifies the object NetWare automounted path whose rights are being checked (cannot be used with the `-p` option) |
| `-p <PATH>` | Specifies the path of the directory for which to list trustee assignments (cannot be used with the `-o` option) |
| `-h` | Displays command help |

You can see what directories on the server `OPENLINUX` the user `jsmith` is a trustee of and what his rights are with the following command:

```
nwboshowtrust -o /NetWare/bindery/OPENLINUX/objects/JSMITH
```

To see which bindery objects are trustees of the `SYS:groups\acctg` directory on the OpenLinux NetWare server, issue the following command:

```
nwboshowtrust -p /NetWare/bindery/OPENLINUX/volumes/SYS/groups/acctg
```

The `xnwbotrustees` utility can also be used to view the trustees of a directory. You can do this with the following command:

```
xnwbotrustees -p /NetWare/bindery/OPENLINUX/volumes/SYS/groups/acctg
```

In addition, the `xnwbotrustees` utility can be used to make rights assignment changes and to make new trustee assignments.

## Viewing NetWare Bindery Object Properties

The `nwboprops` utility enables you to view the properties for a specified bindery object. The following syntax is used:

```
nwboprops -o <PATH>
```

The `<PATH>` is a NetWare automounted path for the bindery object you are querying.

To view the attributes for user object `jsmith` in the `OPENLINUX` NetWare server bindery, issue the following command:

```
nwboprops -o /NetWare/bindery/OPENLINUX/objects/JSMITH
```

## Viewing NetWare Bindery Object Property Values

You can view a bindery object's property values with the `nwbpvalues` utility. The following syntax is used (Table 28.23 shows the possible command-line options for the `nwbpvalues` utility):

```
nwbpvalues [OPTIONS]
```

**Table 28.23 — Command-Line Options for nwbpvalues**

| Options | Description |
|---|---|
| `-o <PATH>` | NetWare automounted path for NetWare bindery object being queried |
| `-p <PROPERTY>` | Property of object being queried |
| `-h` | Displays command help |

To view the Surname property value for user `jsmith` in the `OPENLINUX` NetWare server bindery, issue the following command:

```
nwbpvalues -o /NetWare/bindery/OPENLINUX/objects/JSMITH -p Surname
```

## Creating a NetWare Bindery Object

Two utilities that can be used to create bindery objects are `nwbocreate` and `xnwbocreate`. The following syntax is used (Table 28.24 shows the possible command-line options for `nwbocreate`):

```
nwbocreate [OPTIONS]
```

```
xnwbocreate
```

**Table 28.24 — Command-Line Options for `nwbocreate`**

| Options | Description |
|---|---|
| `-s <PATH>` | NetWare automounted path of server where object will be created. |
| `-o <NAME>` | Name of object that will be created. |
| `-t <TYPE>` | NetWare bindery object type to be created—type is an integer between 1 and 3. Possible types are:<br>1 = User<br>2 = Group<br>3 = Print Queue |
| `-H <PATH>` | NetWare-automounted path to HOME DIRECTORY (only applicable for user objects). |
| `-h` | Displays command help. |

You can create a user object called `john` in the `OPENLINUX` NetWare server bindery with the following command:

```
nwbocreate -s /NetWare/bindery/OPENLINUX -o john -t 1 -H /NetWare/bindery/OPENLINUX/volumes/SYS/users/john
```

Notice that you are creating a home directory for the user `john` at the same time that the account is being created.

The `xnwbocreate` utility gives a graphical interface for adding a NetWare bindery object. The following syntax is used:

```
xnwbocreate -s <SERVER> -t <TYPE>
```

The `<SERVER>` and `<TYPE>` follow the same rules as `nwbocreate` (see Table 28.24).

To create a user object named `mary` in the `OPENLINUX` NetWare server bindery, issue the following command:

```
xnwbocreate -s /NetWare/bindery/OPENLINUX -t 1
```

When the graphical interface appears, use the following steps to achieve the desired results:

1. Type the username in the **New User Name** field.
2. Type the Home Directory path in the **Home Directory Path** field. Note that this path is relative to the server, and not to the NetWare automounted path; therefore, a sample home directory path for `mary` is `sys/users/mary`.
3. Click the **Create** button.

## Modifying Bindery Object Property Values

The two utilities available to modify property values of a bindery object are `nwbpadd` and `xnwboadmin`. The following syntax is used (Table 28.25 shows the possible command-line options for the `nwbpadd` utility):

```
nwbpadd [OPTIONS]

xnwboadmin -o <PATH>
```

**Table 28.25 — Command-Line Options for nwbpadd**

| Options | Description |
|---|---|
| `-o <PATH>` | NetWare automounted path of object to be modified |
| `-p <PROPERTY>` | Object attribute to be modified |
| `-v <VALUE>` | Value for the attribute being modified |
| `-t <TYPE>` | Option for the property being added—valid types are as follows:<br><br>`SET` = Add value to property specified with the `-p` option (can only be used in properties of type SET)<br><br>`STRING` = Is used literally as the new value for the property specified with the `-p` option (can only be used in properties of type ITEM)<br><br>`SEGMENT` = Hexadecimal value to be translated and stored as a byte stream value<br><br>You can view the property type by using the `nwboprops` command and looking at the third column |
| `-h` | Displays command help |

> Note: All options (except `-h`) are required for the `nwbpadd` command.

To modify the Surname property value for the user `jsmith` in `OPENLINUX` NetWare server bindery, issue the following command:

```
nwbpadd -o /NetWare/bindery/OPENLINUX/objects/JSMITH -p SURNAME -t STRING -v Smith
```

The graphical utility `xnwboadmin` enables you to add and edit values for bindery object properties of a specified object.

To edit the properties of `jsmith` in the `OPENLINUX` NetWare server bindery, issue the following command:

```
xnwboadmin -o /NetWare/bindery/OPENLINUX/objects/JSMITH
```

When the graphical utility opens, you can select the property that you want to edit, make the changes using the **Edit Property Value** field, and then click the **Add Value** button.

## Changing Bindery User Passwords

A NetWare user with supervisor privileges can change another user's password with the previously explained `nwpasswd` command:

```
nwpasswd -s <SERVER> -u <USER>
```
