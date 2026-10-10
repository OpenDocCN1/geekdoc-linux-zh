The Novell Directory Service (NDS) is a great help for organizing large networks. NDS is a database of objects, where each object represents users or resources in a network. Within each object is stored information about the individual user or network resource as well as which relations this objects has to other objects in the network. The bindery is a special database; it stores network configuration information on a Novell fileserver. Netware clients query the bindery to get information on available services, users, and routing information.

The Caldera NetWare client provides many NetWare NDS tree and bindery administration utilities. For the NDS tree, these are

+   nwdscrcate  Creates a new NDS object.

+   nndsattribs  Lists attributes of an NDS object's class.

+   nwdsvalues  Lists values of an NDS object's attribute.

+   nndsmmodify  Modifies values of an NDS object's attribute.

+   nndsrm  Removes an NDS object from the tree.

+   nndswaddtrust  Gives an NDS object rights to a NetWare directory.

+   nndsshowtrust  Displays NDS object rights for NetWare directories.

+   nndssespace  Sets the disk quota for a specific NDS directory.

+   nndsshowspace  Shows the disk quota for a specific NDS directory.

And for the bindery server, these are:

+   nwboocate  Creates a new NetWare bindery object (user, group, or queue).

+   nwbproops  Lists the properties of a NetWare bindery object.

+   nwbpopare  Creates a new property for a NetWare bindery object.

+   nwbpadd  Adds a value to a property of a NetWare bindery object.

+   nwbpopvalues  Lists all values of a property of a NetWare bindery object.

+   nwbrm  Removes a value from a property of a NetWare bindery object.

+   nwbbrm  Removes an object from the NetWare bindery.

+   nwbaddtrust  Gives a NetWare bindery object rights to a NetWare directory.

+   nwbshowtrust  Displays a bindery object's right-top NetWare directories.

+   nwbesetespace  Sets a disk quota for a specific NetWare bindery directory.

+   nwbshowspace  Shows the disk quota for a specific NetWare bindery directory.

To install these NetWare administration utilities, execute the following command, with the floppy inserted and mounted as outlined earlier:

```
rpm -ivh /mnt/floppy/ntutils-static-c1.1-17.1306.rpm
```