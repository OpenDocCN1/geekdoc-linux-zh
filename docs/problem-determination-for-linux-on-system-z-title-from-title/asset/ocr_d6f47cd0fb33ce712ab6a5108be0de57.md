Figure 5-25 illustrates how to check the paging activity from z/VM using the Performance Toolkit. Paging happens if there is a guest that gives overhead in the >2GB> memory area, when pages are migrated between the expanded and the main memory (X>MS and MS>X), and when pages are migrated between the expanded memory area and the disk storage area (X>DS). Large values for the Working Set Size (WSS) also cause paging.

![](bbox=[0.27, 0.24, 0.9, 0.68])

Figure 5-25 Confirming swapping by using z/VM Performance Toolkit

the number of paging (2GB under, ESxCS, CS>ES, ES>Disk) of each user

Working Set Size
the number of pages which are allocated on physical memory.