> **NOTE**: You may see one or more security warnings during the course of this procedure. These are to warn you that someone can potentially view the data you are sending to SWAT. If you are working on your local host or on a private LAN, the risk is minimal.

+   1. From the main SAMBA window, click **Shares**.
+   2. Type the name of the directory that you want to share in the Create Share box, then click **Create Share**.
+   3. Add any of these options:

+   *   **Comment** — A few words to describe the shared directory (optional).
+   *   **Path** — The path name of the directory you are sharing.

+   *   **Guest Account** — If Guest OK is selected, then the user name that is defined here is assigned to users accessing the file system. The nobody user account (which is used only by users who access your computer remotely) is the default user used. (The FTP user is also a recommended value.)

+   *   **Read Only** — If Yes, then files can only be read from this file system, but no remote user can save or modify files on the file system. Select No if you want users to be allowed to save files to this directory over the network.

+   *   **Guest OK** — Select Yes to enable anyone access to this directory without requiring a password.

+   *   **Hosts Allow** — Add the names of the computers that you want to allow access to this file system. You can separate host names by commas, spaces, or tabs. Here are some valid ways of entering host names:
+       *   localhost — Allow access to the local host.
+       *   192.168.74.18 — IP address. Enter an individual IP address.
+       *   192.168.74. — Enter a network address to include all hosts on a network. (Be sure to put a dot at the end of the network number or it won’t work!)
+       *   maple, pine — Enable access to individual hosts by name.
+       *   EXCEPT *host* — If you are allowing access to a group of hosts (such as by entering a network address), use EXCEPT to specifically deny access from one host from that group.

+   *   **Hosts Deny** — Deny access to specific computers by placing their names here. By default, no particular computers are excluded. Enter host names in the same forms you used for Hosts Allow.

+   *   **Browseable** — Indicates whether you can view this directory on the list of shared directories. This is on (Yes) by default.