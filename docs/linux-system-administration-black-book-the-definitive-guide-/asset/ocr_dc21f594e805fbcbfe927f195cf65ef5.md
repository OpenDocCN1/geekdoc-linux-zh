# Table 17.2 Options available to designate how access is allowed in /etc/exports.

| Format | Result | Example |
| :--- | :--- | :--- |
| all_squash | Maps all users accessing the specified export to be anonymous | all_squash |
| anongid | Sets to a specific value the GID used for anonymous access | anongid=540 |
| anonuid | Sets to a specific value the UID used for anonymous access | anonuid=570 |
| async | Tells the NFS server to write data to the disks when it chooses to | async |
| insecure | Allows incoming client requests to come in on any port | insecure |
| no_all_squash | Maps incoming client requests to users through one of the specified methods | no_all_squash |
| no_wdelay | Tells the NFS server to not anticipate other potential write requests; only available when sync is used | no_wdelay |
| no_root_squash | Allows root client requests to be mapped to root on the server machine | no_root_squash |
| ro | Sets the export to read-only status | ro |
| root_squash | Maps root client requests to an anonymous UID and GID | root_squash |
| rw | Sets the export to read-write status | rw |
| secure | Requires client requests to come from a port lower than 1024 on the client machine | secure |
| sync | Tells the NFS server to write data to the disks whenever it first comes available | sync |
| wdelay | Tells the NFS server to anticipate other potential write requests | wdelay |