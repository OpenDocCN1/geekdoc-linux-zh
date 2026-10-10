
| Object Name | Abbreviation | Icon | Description |
| :--- | :--- | :--- | :--- |
| **Profile** | CN= | | Contains login script commands that can be assigned to user accounts. You learn how to use Profile objects with login scripts in Chapter 9. |
| **User** | CN= | | A user object represents a person who uses the network. This object is used to manage and maintain information about the user, including login restrictions and his or her access rights. |
| **Volume** | CN= | | A volume object is used to represent a physical file storage area on a NetWare server. Volume objects are created when a server is installed on the network. |

You can assign values to each property of an object. Some object properties, such as a user’s telephone number or the print queue of a printer object, are multivalued, meaning they can contain more than one entry. Each object has certain property values that are required when the object is created. For example, each user object must be assigned a login and last name value when the user is created. Other property values are optional and can be added later. Throughout this book, you learn how to create and configure many of the leaf objects shown in Table 4-3. In this chapter, you learn about the Admin, volume, and alias leaf objects.

## The Admin User Object

The **Admin user object** is created when the first server is installed in the eDirectory tree. Admin is an important user object because it has Supervisor rights to the entire eDirectory tree, allowing the Admin user to create and manage all other objects in the tree structure. As you learned in Chapter 2, a password is given to the Admin user during the initial server installation. If you’re the Admin user, make sure you remember this password because without it, you must reinstall the eDirectory tree to regain Supervisor rights. Because of the importance of the Admin user account, many organizations create a backup Admin user and then secure this user name and password in a safe place, such as the company vault or safety deposit box. In Chapter 5, you learn how to secure your Admin user account and create a backup Admin user account.

## Volume Objects

As described in Chapter 3, when you create a physical NetWare volume on a server, a **volume object** is created in the eDirectory tree in the same context as the NetWare server it resides on. The volume object acts as a pointer to a physical volume object and contains status and configuration information for the volume (see Figure 4-11).

The volume object name defaults to a combination of the server’s name and the volume’s physical name separated by an underscore. For example, a server named UASHOST in the UAS Organization has a physical volume named CORP. The default volume object for the CORP physical volume is created in the UAS Organization with the name UASHOST_CORP. Because the eDirectory volume object acts as a pointer to the volume’s physical data, often it’s convenient to create additional volume objects for a physical volume in other containers. For example, if users in the Engineering and Management containers access data from the CORP volume, volume objects that point to the CORP volume can be created in both the Engineering and Management containers. These volume objects can be given the same or different names. For example, you can name the volume object in the Engineering container EngCorpVol and then point it to the CORP volume on the UASHOST server.

![](img/840007e8f98ea6653e5877e945c27dc6_155_0.png)

**Figure 4-11** Volume object properties

## Alias Objects

You can have multiple eDirectory volume objects for a single physical volume, but most other object types, such as servers, printers, and users, can be represented by only one eDirectory object. So if you want to access a printer or server object from another container, you need to select that printer or server object by navigating to the container holding the object or by typing its distinguished name as described in the next section. Alias objects can be used to simplify access to objects in other containers. The **alias object** holds no data about the original object; it acts only as a pointer. For example, users in the IT Department frequently need to access the server object to check configuration data. Instead of requiring users to navigate the eDirectory tree to locate the actual server object, you can create an alias object in the IT container that points to the actual server object in the UAS container. In the next section, you learn how to create an alias object for your UASHOST server.

## Directory Map Objects

Moving data directories to other volumes or servers is sometimes done because volumes fill up or new servers are added to the network. Moving a data directory to a new location can require a lot of maintenance on the network administrator’s part to find and change drive mappings on many user computers. **Directory Map objects** offer an alternative by storing the physical path to a data directory, as shown in Figure 4-12. When a data directory is moved to a new location, the network administrator needs to change only the path in the Directory Map object.

For example, in Figure 4-12 the Path property of the Directory Map object called Shared can be changed to point to the ENGDATA volume on the ENGHGHOST server. Because drive L: on the client computer is mapped through the Shared object, when the path is changed to the ENGDATA volume, the user is directed to that directory without making any changes to the client computer’s drive settings. In Chapter 7, you learn how to create Directory Map objects.

![](img/840007e8f98ea6653e5877e945c27dc6_156_0.png)

**Figure 4-12** A Directory Map object

## Object Naming

Each object in the eDirectory tree is given a name known as its **common name (CN)**. An object’s common name must be unique within the container that houses the object. In addition to a common name, each eDirectory object has a context. Just as a path is used to specify a file location on a disk drive, the **context** specifies the location of an object in an eDirectory tree. One difference between a path to a file location and an eDirectory context is that the context is indicated with X.500 notation, which starts with the object and works up the tree. In contrast, a disk path is specified from the root of the drive down to the file name. For example, to identify the path to the Memo file in the Document directory of the C: drive, you use `C:\Document\Memo`, but to identify the context of the user EKenton in the IT container shown previously in Figure 4-9, you use `.EKenton.IT.UAS`. Another difference between an eDirectory context and a path is that the eDirectory context is formatted with periods to separate each level instead of the slashes or backslashes used in paths. The period at the beginning of the context specifies starting at the root of the eDirectory tree in much the same way that a slash is used at the beginning of a path.

Each object in the eDirectory database can be uniquely identified by its **distinguished name**, which consists of the object’s name and its complete context, leading to the root of the eDirectory tree. A context specification that includes object abbreviations is referred to as *typeful*. For example, the user EKenton could be identified by using this typeful distinguished name:

```
.CN=EKenton, OU=IT, O=UAS
```

The two-letter abbreviation preceding the name of an object identifies the object’s type. For example, CN= identifies EKenton as the common name for a leaf object, the OU= identifies IT as an Organizational Unit container object, and the O= identifies UAS as an Organization container object.

Using typeful distinguished names that include the object type abbreviation and the context requires extra time and opens up the possibility of errors. As a result, eDirectory can assume object types as long as the rightmost object is an Organization or Organizational Unit. A distinguished name that doesn’t contain object type abbreviations is referred to as *typeless*. For example, this is the typeless distinguished name for the user EKenton:

```
EKenton.IT.UAS
```

When you log in to eDirectory, your client computer is assigned to a location in the eDirectory tree structure in much the same way that your command prompt is assigned a position in the file system when you open a command prompt window. The default location of your client computer in the eDirectory tree is referred to as its **current context**. By setting the client’s current context during the login process, you make it easier for
