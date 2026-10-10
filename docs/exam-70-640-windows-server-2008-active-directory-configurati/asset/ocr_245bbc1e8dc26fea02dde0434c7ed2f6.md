![](bbox=[0.85, 0.03, 0.98, 0.13])

LESSON

# # Global Catalog and Flexible Single Master Operations (FSMO) Roles

# ## OBJECTIVE DOMAIN MATRIX

| TECHNOLOGY SKILL | OBJECTIVE DOMAIN | OBJECTIVE DOMAIN NUMBER |
| :--- | :--- | :---: |
| Configuring Additional Global Catalog Servers | Configure the global catalog. | 2.5 |
| Placing FSMO Role Holders | Configure operations masters. | 2.6 |

# ## KEY TERMS

cached credentials  
clock skew  
Domain Naming Master  
_gc  
indexed  
Infrastructure Master

partial attribute set (PAS)  
Primary Domain Controller (PDC) Emulator  
relative identifier (RID)  
Relative Identifier (RID) Master  
Schema Master

security identifier (SID)  
seize  
transfer  
universal group  
universal group membership  
caching

Margie's Travel is a national chain of booking agencies for resort hotels throughout Europe and the Caribbean. It relies heavily on Active Directory to provide authentication for its many database and intranet applications. Margie's Travel uses a multidomain Active Directory forest containing an empty forest root domain and several child domains representing the geographical regions served by the different offices. Because of the multidomain nature of the Margie's Travel Active Directory infrastructure, the Margie's Travel IT staff needs to strictly maintain access to global catalog servers and Flexible Single Master Operations (FSMO) role holders across the entire organization.

After completing this lesson, you will be able to discuss the global catalog server and the critical role that it plays within Active Directory. You will understand the importance of proper placement of global catalog servers within an Active Directory forest and how to add and remove global catalogs from your network. You will also be able to discuss a feature known as universal group caching, which can reduce the reliance on global catalog servers in certain environments where it might not be feasible to deploy as many as you require. Finally, you will be able to describe the Flexible Single Master Operations (FSMO) roles, and the functions that they perform within an Active Directory domain and forest. Through the exercises and information presented in this lesson, you will be able to plan the optimum placement of FSMO roles within your environment as well as to deploy, transfer, and seize FSMO roles in the event of temporary or permanent failure of one or more domain controllers within your Active Directory domain or forest.