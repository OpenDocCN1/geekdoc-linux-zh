# Export vCenter Server Inventory Items

An alternate approach to backing up your complete vCenter Server database is exporting the specific database objects that are of importance in your environment. Using this approach, you can restore your inventory (or maybe just a part of your inventory) to a separate database for testing purposes or create a disaster recovery (DR) replica of your inventory on another vCenter Server. Using this approach, you can even restore your vCenter Server environment to a vCenter Server that is using a different database platform for the backend.

We encountered an environment where, due to a database move, the SQL agent rollup jobs were unavailable. The person moving the database was unaware of the existence of any SQL agent rollup jobs. As a result, the real-time performance statistics were consolidated. By the time someone noticed there was something wrong with the performance charts, the database had grown very, very large. Performance was degrading, and statistics were being deleted from the database.

Using a script provided by VMware would have required vCenter Server to be offline for a number of days. Restoring the database from backup was not an option either, since it was a very dynamic environment. The backup was several weeks out-of-date. A restore would result in the loss of many changes, which

In the end, we used the functions discussed next to re-create the database overnight at the cost of losing all the performance data. But, since the performance statistics were corrupted, we were more than willing to pay that price. It beat having the vCenter Server for several days. After the rebuild process was done, these functions were still being used to replicate some parts (like roles, permissions, and folders) to a DR environment on a regular basis.

Although this sounds great, the structure of the vCenter Server inventory is complex and contains many different object types and configuration items that are linked to each one way or the other. To show how you can export all possible objects in your inventory would make this chapter nearly 100 pages or more, so we'll stick to the most common objects to give you an idea of the possibilities.

# Folders

We start at the top of the inventory, the root folder, and retrieve the complete folder structure of your environment. The folder structure is the logical layout of your environment, and because folders function as containers for other objects, they are an essential part of your environment. The root folder object is the only