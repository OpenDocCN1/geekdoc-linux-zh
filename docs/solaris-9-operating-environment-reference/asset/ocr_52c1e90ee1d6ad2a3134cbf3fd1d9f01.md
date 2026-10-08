Each of these rights can be granted to any one of four different categories.

owner Grant a right to the owner of an object. The owner is the NIS+ principal identified in the owner field. The owner can be changed with the nischown(l) command. Note that if the owner does not have modification access rights to the object, he cannot change any access rights to the object unless he has modification access rights to its parent object.

group owner Grant a right to the group owner of an object. This grants the right to any principal that is identified as a member of the group associated with the object. The group owner can be changed with the nischgrp(l) command. The object owner need not be a member of this group.

world Grant a right to everyone in the world. This grants the right to all clients who have authenticated themselves with the service.

nobody Grant a right to the nobody principal. This has the effect of granting the right to any client that makes a request of the service, regardless of whether the client is authenticated.

Note that for bootstrapping reasons, directory objects that are NIS+ domains, the org_dir subdirectory, and the cred table within that subdirectory must grant access to the nobody principal. This permission makes navigation of the namespace possible when a client is in process of locating its credentials. Granting this access does not enable the contents of other tables within org_dir to read (such as the entries in the password table) unless the table itself gives "real" access rights to the nobody principal.

# Directory Authorization

Additional capabilities grant access rights to clients for directories. These rights are contained within the object access rights (OAR) structure of the directory. This structure enables the NIS+ service to grant rights that are granted by the directory object obtained of a specific type.

An example of this capability is a directory object that does not grant access to all clients but does create access in the OAR structure for objects of type group to clients who are members of the NIS+ group associated with the directory. In this, the only objects that could be created as children of the directory would have of the type group.

Another example is a directory object that grants access only to the owner of the directory and then additionally grants access through the OAR structure for objects of type table, link, group, and private to any member of the directory's group. The group gains nearly complete access to the group with the exception of creating subdirectories. The creation of new NIS+ domains are restricted because creating both requires creating groups_dir and org_dir subdirectory.

> Note — There is no command-line interface to set or change the OAR of the directory object.

# Table Authorization

As with directories, additional capabilities are provided for granting access to entries within tables. Rights granted to a client by the access rights field in a table object to the table object and all of the entry objects "contained" by that table. If an access right