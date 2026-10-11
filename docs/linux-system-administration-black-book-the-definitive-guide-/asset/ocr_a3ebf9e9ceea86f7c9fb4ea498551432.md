Table 18.6   Popular options used in individual Samba share definitions.

| Option | Purpose | Value(s) | Example |
| :--- | :--- | :--- | :--- |
| **admin users** | Sets a list of users who access this share with superuser-like privileges. Strong security implications arise when you utilize this option, because not only do you allow the defined users to have the power to empty the share, change permissions, and more, but if an intruder gains access using one of these accounts, that intruder can alter the files as they see fit. | A space-separated list of users | **admin users = joe barb** |
| **browseable** | Specifies whether to allow Samba clients to see this share when requesting a list of shares available. | **yes** or **no** | **browseable = yes** |
| **case sensitive** | Specifies whether Samba handles file names as case-sensitive or ignores case entirely. | **yes** or **no** | **case sensitive = no** |
| **copy** | Tells Samba to copy all parameters from another share, and override those that are duplicated in this share. | Share name with no brackets | **copy = ProjectB** |
| **default case** | Sets the default case for file names created by clients. | **upper** or **lower** | **default case = lower** |
| **dont descend** | Explicitly refuses to allow Samba clients to access particular subdirectories. | A comma-separated list of subdirectories | **dont descend = /Projects/ProjectB/needs_approval** |
| **follow symlinks** | Tells Samba whether to follow symbolic links out of the share. | **yes** or **no** | **follow symlinks = no** |
| **force group** | Sets all users accessing this share to belong to the listed group. | Group name, or **+group** if you want only users who are already assigned to this group to create files under the group's name | **force group = project_staff** |

(continued)