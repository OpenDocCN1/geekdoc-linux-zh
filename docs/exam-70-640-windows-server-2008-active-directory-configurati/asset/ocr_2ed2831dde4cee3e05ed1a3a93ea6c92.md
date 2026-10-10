# **Table 5-1 (*continued*)**

| **GROUP NAME** | **GROUP SCOPE** | **LOCATION IN ACTIVE DIRECTORY** | **DEFAULT MEMBERS** | **PURPOSE** | **SPECIAL NOTES** |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Domain Computers | Global | Users container | Members include all workstations and servers joined to the domain and any computer accounts manually created. | Any computer account created in a domain is automatically added to this group. The group can be used to make computer management easier through group policies. (Refer to Lessons 7 through 10.) | None |
| Domain Controllers | Global | Users container | Members include all domain controllers within the respective domain | All computers installed in the domain as domain controllers are automatically added to this group. | None |
| Domain Guests | Global | Users container | Guest account | Members include all domain guests. | None |
| Domain Users | Global | Users container | User account created in a domain is automatically added to this group | Members include all domain users. This group can be used to assign permissions to all users in the domain. | None |
| Enterprise Admins (appears only on forest root domain controllers) | Universal | Users container | Administrator user account for the forest root domain | This group is added to the Administrators group on all domain controllers in the forest. This allows the global administrative privileges associated with this group, such as the ability to create and delete domains. | None |
| Enterprise Read-Only Domain Controllers | Universal | Users container | None | This group contains all Read-Only Domain Controllers within an entire forest. | None |
| Group Policy Creator Owners | Global | Users container | Administrator user account for the domain | Members can modify group policy for the domain. | None |
| RAS and IAS Servers | Domain local | Users container | None | Servers in this group—for the Remote Access Service (RAS) and Internet Authentication Service (IAS)—are permitted access to the users' remote access properties. | None |

(*continued*)