# ## Telling the NFS Server Process About /etc/exports

Once you have an /etc/exports file written up, use the exports command to tell the NFS server processes to re-read the configuration information. The parameters for exports are as follows:

| **exports Command Option** | **Description** |
| :--- | :--- |
| -a | Export all entries in the /etc/exports file. |
| -r | Re-export all entries in the /etc/exports file. |
| -u *client:/dir/to/mount* | Unexport the directory /dir/to/mount to the host *client*. |
| -o *options* | Options specified here are the same as described in Table 18-1 for client permissions. These options will apply only to the file system specified on the **exportfs** command line, not to those in /etc/exports. |
| -v | Be verbose. |
| -i | Ignore /etc/exports file. |

Following are examples of exportfs command lines.

+   *   To export all file systems:
+   
+       ```bash
+       [root@ford /root]# exportfs -a
+       ```
+   *   To export the directory /export/stuff to the host taos, with the read/write and no_root_squash permissions:
+   
+       ```bash
+       [root@ford /root]# exportfs -o rw,no_root_squash taos:/export/stuff
+       ```

> > **NOTE:** In most instances, you will simply want to use **exportfs -r**.

# ### Common Problems

When exporting file systems, you may find that the server appears to be refusing the client access, even though the client is listed in the /etc/exports file. Typically, this happens because the server takes the IP address of the client connecting to it and resolves that address to the Fully Qualified Domain Name (FQDN), and the hostname listed in the