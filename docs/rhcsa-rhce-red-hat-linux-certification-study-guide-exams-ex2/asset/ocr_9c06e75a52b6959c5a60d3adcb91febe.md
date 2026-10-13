Other parameters relate to how users are treated for the purpose of NFS shared directories. As shown in Table 16-2, the options are associated with the root administrative user, anonymous-only users, and other users that may be designated in the parameters.

# Activate the List of Exports

It's not enough to configure the /etc/exports file, as it's simply the default set of exported directories. You need to activate them with the exportfs -a command. The next time RHEL 6 is booted, if the right services are activated, the nfs start script (/etc/init.d/nfs) automatically runs the exportfs -r command, which re-exports directories configured in /etc/exports.

However, if you're modifying, moving, or deleting a share, it is safest to temporarily unexport all filesystems first with the exportfs -ua command before reexporting the shares with the exportfs -a command.

Once exports are active, they're easy to check. Just run the showmount -e command on the server. To review the export list for a remote NFS server, just add the name of the NFS server. For example, the showmount -e server1.example.com command looks for the list of exported NFS directories from the server1.example.com system. If this command doesn't work, communication may be blocked with a firewall.

# Special Requirements for /home Directories

Some systems store user /home directories on a central server. Such directories can be shared via NFS. Administrators can then back up the /home directories on a regular basis, perhaps supplemented by configuration in a RAID array. That works

TABLE 16-2
NFS Tool User Access Options

| Parameter | Corresponding /etc/exports Command / Description |
|---|---|
| no_root_squash | Treat remote root user as local root; remote root users get root privileges on the shared directory. |
| all_squash | Treat all client users as anonymous users; all remote users are mapped as an anonymous user. |
| anonuid=user id | Specify local user ID for anonymous users; supports mapping of remote users to a specific user ID such as guest. |
| anongid=user id | Specify local group ID for anonymous groups; supports mapping of remote groups to a specific group ID. |