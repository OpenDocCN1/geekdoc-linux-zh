TABLE A.12 Continued
| Type | Code | Description |
| :--- | :--- | :--- |
| 132 | 0 | Group membership reduction |
| 133 | 0 | Router solicitation |
| 134 | 0 | Router advertisement |
| 135 | 0 | Neighbor solicitation |
| 136 | 0 | Neighbor advertisement |
| 137 | 0 | Redirect |

# IPv6 Multicast Scope Field

Table A.13 defines the different values for the scope field in the multicast IPv6 addresses.

TABLE A.13 IPv6 Multicast Scope Field Descriptions
| Scope | Range | Description |
| :--- | :--- | :--- |
| 0 | (undefined) | |
| 1 | Node | Local on the same host (like 127.0.0.1). |
| 2 | Link | Messages stay within the router's group. The routers never let these messages pass through. |
| 3–4 | (undefined) | |
| 5 | Site | As defined by the network administrators, the messages stay within the site's locality. |
| 6–7 | (undefined) | |
| 8 | Organization | As defined by the network administrators, the messages stay within the organization's locality. |
| 9–13 | (reserved) | |
| 14 | Global | All routers permit messages to pass through the global network until they expire. |
| 15 | (reserved) | |