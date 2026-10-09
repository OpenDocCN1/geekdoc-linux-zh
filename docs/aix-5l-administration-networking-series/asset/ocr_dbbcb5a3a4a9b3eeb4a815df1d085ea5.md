# CHECKLIST

The following is a checklist for the key points in AIX Runtime Configuration:

+   - If you are not comfortable using the command-line options, you can use the SMIIT FastPath `smit shutdown` to stop the system and send a message to all users.

+   - Set the correct date and time zone by invoking the SMIT FastPath `smit chtz_date`.

+   - You can add more languages to the set with the `smit mlang` command.

+   - You can alter AIX kernel characteristics for the maximum number of processes allowed per user, the maximum number of pages in block I/O buffer, the amount of real memory that can be pinned for network MBUFFS, and other memory and scheduler subsystems using the SMIT FastPath `smit chgsys`. Be careful making changes to the system on this panel!

+   - To alter the number of licensed users, run the SMIT FastPath `smit chlicense`.

+   - You can broadcast a message to all logged-on users using the SMIT FastPath `smit wall` command.

+   - Monitor the `/var/adm/ras/errlog` log file regularly to scan for intermittent system problems using the `errpt` command..

+   - Manage the system logs from the SMIT FastPath `smit logs`.

+   - In most large environments, you should define a dedicated dump device as the primary dump device rather than the AIX 4.3 and 5L default of the `/dev/hd6` paging space. Access the SMIT dump menu with the SMIT FastPath `smit dump`.

+   - You have at least three options for a user interface, depending on the software installed on the server. You can use the SMIT FastPath `smit ditconfig` to select between ASCII, CDE, and CDE with ASDL during boot.

+   - To activate the Remote Reboot Facility, use the SMIT FastPath `smit rrbty`.

+   - In AIX 5L, Use the SMIT FastPath `smit shd` to set up hang detection to determine how the system will react to a hang condition.