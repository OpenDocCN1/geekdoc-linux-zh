The File Browser Settings page contains the following options:

+   - *Navigation Panel Icon (KDE only)*—Enables or disables the File Browser Navigation Panel icon. This icon is displayed only in KDE.
+   - *Novell Properties*—Enables or disables the Novell Properties menu option when users right-click a Novell file system directory or file in a file manager.
+   - *Purge Novell Files*—Enables or disables the Purge Novell Files menu option when users right-click a Novell file system directory or file in a file manager.
+   - *Salvage Novell Files*—Enables or disables the Salvage Novell Files menu option when users right-click a Novell file system directory or file in a file manager.
+   - *File and Folder Information*—Enables or disables the File Information and Folder Information tabs on the File and Folder Properties pages (available when users right-click a Novell file system directory or file in a file manager and then select Novell Properties).
+   - *Novell Rights*—Enables or disables the Novell Rights tab on the File and Folder Properties pages (available when users right-click a Novell file system directory or file in a file manager and then select Novell Properties).
+   - *Volume Information*—Enables or disables the Volume Information tab on the Volume Properties page (available when users right-click a Novell file system directory or file in a file manager and then select Novell Properties).
+   - *Volume Statistics*—Enables or disables the Volume Statistics tab on the Volume Properties page (available when users right-click a Novell file system directory or file in a file manager and then select Novell Properties).

# Configuring OpenSLP Settings

Use the Service Location Protocol (OpenSLP) Settings page in the Novell Client Configuration Wizard to specify where and how the client requests network services.

In an IP-only network, the Novell client needs a way to resolve the eDirectory tree, context, and server names to an actual IP address of an eDirectory server that can provide authentication. On a simple LAN, the client can send an IP broadcast to discover this information, but on a multiple site WAN, the SLP scope and Directory Agents must be listed. See Figure 13-28.