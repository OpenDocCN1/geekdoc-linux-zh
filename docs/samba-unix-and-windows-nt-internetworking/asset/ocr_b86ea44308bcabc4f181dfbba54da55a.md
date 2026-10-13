announcements; if '0', no announcements will be made.

# Election Parameters

| Parameter | Description |
|---|---|
| `browse list = <yes, no>` | Will server support browse lists? |
| `announce as = <NT, Win95, WfW>` | OS type Samba will announce. |
| `announce version = <version number>` | OS version Samba will announce. Default 4.2 is higher than 4.0 announced by NT. |
| `os level = <integer>` | OS level for election criteria; a value of '65' will exceed NT Server. |
| `local master = <yes, no>` | Indicates if Samba should try to become local master. |
| `preferred master = <yes, no>` | Indicates that Samba will force an election on startup and attempt to become a master browser. Used to weight browser election in Samba's favor. |
| `domain master = <yes, no>` | Samba is domain master and will collate and synchronize browse lists between local master browsers. DO NOT USE IF AN NT PDC ALREADY EXISTS FOR THE DOMAIN. |

# Share and List Parameters

| Parameter | Description |
|---|---|
| `auto services = <list>` | The set of local share names you want added to the browse list |
| `browsable = <yes, no>` | Is this share browsable? |
| `comment = <text>` | Share description for browse lists |