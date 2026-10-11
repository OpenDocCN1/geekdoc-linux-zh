Rollback segments are also referred to as *undo segments* because they are used to *undo* a transaction when a ROLLBACK command is issued.

Like any other database segment, rollback segments are made up of extents, which are in turn comprised of five or more contiguous Oracle blocks. Within each rollback segment, Oracle uses the extents in a circular fashion until the rollback segment is full. Once the rollback segment is full, no new transactions will be assigned to it until some of the rollback segment space is released when a user issues a COMMIT or ROLLBACK command. A single rollback segment can store the before-images for several different transactions. However, a transaction writes its before-image information to only one rollback segment. Figure 8.23 illustrates this concept for a rollback segment called RBS01, which is made up of eight extents.

# **FIGURE 8.23** How transactions use rollback segments

![](bbox=[0.24, 0.5, 0.88, 0.8])

Figure 8.23 shows that two transactions, A and B, are both storing their before-images in extent 1 of rollback segment RBS01, while a larger transaction (C) is using extents 2 through 6 to store its undo information. Extents 7 and 8 are currently inactive.