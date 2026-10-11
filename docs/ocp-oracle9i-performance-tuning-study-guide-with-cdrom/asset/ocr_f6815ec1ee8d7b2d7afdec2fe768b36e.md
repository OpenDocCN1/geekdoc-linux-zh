As shown in Figure 8.13, each block is divided into three sections:

+   Block header area

+   Reserved space

+   Free space

These areas, used in conjunction with the Percent Free (**PCTFREE**) and Percent Used (**PCTUSED**) parameters, help determine how the block is used to store data.

# ## Block Header Space

Every segment block uses some of its allocated space to store header information about the contents of that block. This header information includes the transaction slots specified by the **INITRANS** parameter at table creation, a directory of the rows that are contained within the block, and other general header information needed to manage the contents of the block. This block header information generally consumes between 50 to 200 bytes of the block's total size.

# ## Reserved Space

The parameter **PCTFREE** tells Oracle how much space to set aside in each block to store row updates. This value is specified as a percentage of the overall size of the block. For example, if you create a table with a **PCTFREE** setting of 20, then 20 percent of the block's storage will be set aside to hold updated row information. Once a block is filled with data to the level of **PCTFREE**, the block will no longer accept new inserts, leaving the remaining space to store updates to the existing rows already stored in the block.

The process of removing a block from the list of available blocks is performed by the table's *Free List*. You can think of a Free List as a clipboard that contains a listing of the block IDs that belong to a particular segment. Whenever a user's Server Process wants to insert a new row into a segment, the Server Process consults the Free List to find the block ID of a block that is available to accept the insert. If the subsequent insert should cause the block to fill to above the cutoff determined by **PCTFREE**, then the block is taken off the Free List, and no other inserts will be made to that block.

A block stays off the Free List until enough data is deleted so that the block's available space falls below that specified by **PCTUSED**. When this occurs, the block will go back to the top of the Free List where it can be used again to store new inserts. The default values for **PCTFREE** and