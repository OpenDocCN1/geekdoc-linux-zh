# # Placing FSMO Role Holders

> When you install the first domain controller in a new forest, that domain controller holds both of the forest-wide FSMOs as well as the three domain-wide FSMOs for the forest root domain. Although this default location may be sufficient for a single-site design, a forest containing numerous domain controllers or sites may require you to transfer some of the roles to different domain controllers.

Planning the appropriate locations for FSMO role holders requires that you consider the following design aspects:

+   - The number of domains that are or will be part of the forest
+   - The physical structure of the network
+   - The number of domain controllers that will be available in each domain

Each of these factors will assist you in deciding where to place FSMO roles to achieve the best possible performance, accessibility, and fault tolerance for your Active Directory environment. In addition, you must know which domain controllers might be able to take over a FSMO role for a server if the server is temporarily or permanently offline.

As discussed, when you create the first domain in a new forest, all of the FSMO roles are automatically assigned to the first domain controller in that domain. Figure 4-3 shows a simple design and the default locations for the global catalog and all five FSMO roles.

![](bbox=[0.0, 0.48, 0.65, 0.8])