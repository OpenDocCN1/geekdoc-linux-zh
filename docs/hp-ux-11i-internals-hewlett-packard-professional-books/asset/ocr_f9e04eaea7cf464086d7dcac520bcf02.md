![](bbox=[0.05, 0.1, 0.95, 0.38])

# **Figure 7-2 Inside Each pregion**

In this simplified model we see that all the pages of the **pre gion** are arranged in a circle, and their respective **vfd s** appear as the numerals on the face of a clock. In our simple example, the **p region** has 32 pages, sufficient to explain **vh and** operation. In the **p region** structure, the **p_stealscan** points to the next page in this **p region**, which may be checked for parole. The **p_agescan** points to the next page **vh and** may age. When **vh and** enters a **p region**, it is only allowed to scan 1/16 of the available pages.

The **p_stealscan** must lag the position of the **p_agescan** by [**(p_count/16) * handlaps]**. Maintaining this lag assures that a process that still needs the aged page may access it before it is stolen. The larger the lag, the less likely **vh and** is to steal a page in current use.

The next time the system points to this **pregion**, the next 1/16 of its pages may be scanned. Individual **pregions** are dual-linked in a systemwide list of all active **pregions** by their **p_forw** and **p_back** pointers

# **The Linked pregion List**

The kernel follows this dual-linked list to find the next **pregion** to scan Figure 7-3 illustrates this concept. You can think of the operation as a two-level clock. The hands on the main clock are the system's **agehand** and **stealhand**. Inside each **p region** are corresponding **p_agescan** and **p_stealscan** pointers. This is where the paging routine's name comes from: **vh and** stands for the *virtual hand* pager.