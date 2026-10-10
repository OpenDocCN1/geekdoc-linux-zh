**Hack State:** Remote control.

**Vulnerabilities:** NetWare NDS.

**Breach:** After gaining access control to the NetWare O/S, hackers attempt to install a remote-control backdoor that may go unnoticed for some time. There are six simple steps to initiate this process:

+   1.  In NWADMIN, highlight an existing container.
+   2.  Create a new container inside this container.
+   3.  Create a user inside this new container.
+       a) Allow full trustee rights to this user's own user object.
+       b) Allow this user full trustee rights to the new container.
+       c) Give this user supervisory equivalence.
+   4.  Modify the Access Control List (ACL) for the new user so that he or she cannot be seen.
+   5.  Adjust the Inherit Rights Filter on the new container so it cannot be seen.
+   6.  Place the new container in the IT group container to install the backdoor ard to enable its login to show up in the normal tools that show active connections.

Locking Files

**Synopsis:** Inside and local hackers can wreak havoc by modifying file usability.

**Hack State:** File control.

**Vulnerabilities:** NetWare 2x, 3x, 4x, IntraNetWare 4x.

**Breach:** After gaining access to NetWare, some hackers are keen on causing chaos by locking files. This hack attack, associated with a program called Bastard by The Grenadier (Underground hacker/programmer) (Figure 10.18), is popular among disgruntled employees. Basically, upon execution, the program simply asks for the path to a file for lockdown modifications. At that point, no other user can open the file for use until the attacker closes *Bastard.exe*, logs off, or shuts down. Essentially, when critical O/S operational files fall victim to this exploit, this brings networks to their knees. The program is almost too simple to use: the only requirement is that the attacker have Read access to the target file.

![](bbox=[0.13, 0.65, 0.74, 0.79])

**Figure 10.18** Locking files with Bastard.

Miscellaneous Mayhem

Disappearing Disk Usage

**Synopsis:** Hackers can crash hard drives by filling up all available space.