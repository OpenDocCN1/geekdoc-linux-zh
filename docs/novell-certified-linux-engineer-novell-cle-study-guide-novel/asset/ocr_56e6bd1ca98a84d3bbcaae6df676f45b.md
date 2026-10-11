+   ▶ **Compare**—The compare property right allows the trustee to query the value of the specified property using a Boolean expression. For example, you could query the object to see if its phone number value is equal to 555-555-5555. The compare right only returns a TRUE or FALSE response. The compare right doesn't allow you to see the actual value of the property.

+   ▶ **Read**—The read property right allows the trustee to view the value of the specified property. It doesn't allow the trustee to modify the property in any way.

+   ▶ **Write**—The write property right allows the trustee to modify the value of the specified property.

+   ▶ **Add Self**—The add self property right is an interesting one. It allows the trustee limited access to the value of a property. It only allows the trustee to set the value of the specified property to the name of the trustee object (hence the term *add self*).

There's one more key aspect of eDirectory rights that you need to understand: *inheritance*.

# # Managing Inheritance

It is vital that you understand that eDirectory rights, by default, flow down the tree in what is called *inheritance*. The best way to understand inheritance is through an example.

Suppose your organization has grown very large and you need help managing the eDirectory tree. You decide to grant user LMorgan.IFCLE the browse, create, and rename rights to the CLE container in your tree so she can create, delete, and modify objects in the tree.

The rights assignment you made to the CLE container flow down the tree to objects beneath CLE in the hierarchy. In other words, LMorgan.IFCLE receives rights to all other objects below CLE through inheritance. For example, if there is a user object named VHammer in the SLC.CLE context, LMorgan.IFCLE has browse, create, and rename rights to the VHammer.SLC.CLE object, even though she hasn't been explicitly granted rights to it.

Rights that a trustee receives to an object through inheritance and not through an explicit rights assignment are called *effective rights*.

This is how your admin object receives rights to the entire eDirectory tree. Consider Figure 5.29.