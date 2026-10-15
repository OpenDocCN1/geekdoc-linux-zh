Each computer name is followed, without a space, by a list of parameters in parentheses. The options allowed for given hosts include

+   - secure—Requests must originate on a port with a number lower than 1024. This is the default. To turn this option off, use insecure.
+   - ro—Read-only access to the export. This is the default when using knfsd.
+   - rw—Read/write access to the export. This is the default when using nfs-server.
+   - noaccess—Makes all directories below the specified one inaccessible. You must create a separate entry for this option, as in the example on page 245, in which /home/edgar is excluded from the export of /home to the host nessus.
+   - link_relative—Converts absolute symbolic links to relative symbolic links on export.
+   - link_absolute—Leaves symbolic link references as they are. This is the default.
+   - root_squash—Treats accesses from the root user on the remote system as if they came from user nobody, severely limiting write access to the system. This is the default.
+   - no_root_squash—Turns off root squashing. I don’t recommend using this option in most cases.
+   - all_squash—Treats all access requests as if they came from the user nobody, severely limiting write access to the server.
+   - squash_uids and squash_gids—Specifies a list of user or group IDs, respectively, to be squashed. The example on page 244 shows this option in use on the first line of the example.
+   - map_daemon—Remaps user and group IDs, allowing one user to have different user or group IDs on different systems. Requires support from a special daemon on the client system.
+   - map_static—Maps user and group IDs according to the contents of the specified file name. This option is covered in greater detail in the "Configuring a User Map File" section later in this chapter.
+   - map_nis—Maps user and group IDs according to information obtained from an NIS server.

In most cases, you don’t need more than a few of these options in a simple network.