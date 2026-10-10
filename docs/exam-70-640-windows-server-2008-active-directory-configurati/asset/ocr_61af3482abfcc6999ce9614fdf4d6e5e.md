Figure 4-4 illustrates the result of creating a new child domain or the root domain of a new domain tree within an existing forest. The forest-wide FSMOs and the domain-wide FSMOs for the forest root domain remain in place, and the first domain controller in the new domain is automatically assigned the RID Master, PDC Emulator, and Infrastructure Master roles.

# Figure 4-4
Default FSMO placement in a forest with one child domain

![](bbox=[0.31, 0.15, 0.67, 0.71])

As your company grows beyond a single site or physical location, you must consider placement of the FSMO roles that will accommodate growth without compromising accessibility, fault tolerance, or performance. Table 4-2 shows a breakdown of each FSMO role and the recommended guidelines for placement. In this table, two attributes are used to describe a domain controller: highly available and high capacity. As applied to domain controllers operating as FSMO servers, these terms are defined as follows:

+   * **Highly available.** This domain controller is centrally located if possible and contains additional hardware, such as a redundant array of independent disks (RAID) controller. RAID allows a server to keep functioning even if one of the drives in the array experiences a failure.
+   * **High capacity.** This domain controller has a greater processing ability relative to the other domain controllers available. A high-capacity server generally has a faster central processing unit (CPU), more memory, and faster network access.