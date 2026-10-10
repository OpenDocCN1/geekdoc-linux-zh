A similar technique you can use in NetWare 6.5 is to create an Organizational Role object (covered in Chapter 5), and then make it the trustee of a directory or file instead of making a user the trustee. The Organizational Role object can then be assigned to users who need access to the directory or file. If your company does a lot of reorganizing, you might consider using groups or Organizational Role objects instead of assigning rights to users. An effective way to minimize trustee assignments is to make these assignments in the following order:

+   1. Assign rights to containers.
+   2. Assign rights to departmental groups.
+   3. Assign rights to Organizational Role objects.
+   4. Assign rights to individual users.

# Avoid Complex Combinations

The last guideline in planning file system security is to avoid combinations of assignments to groups, containers, and individual users within the same directory structure. To keep things as simple as possible, don't rely on users inheriting certain rights because of membership in certain groups and containers; instead, make users explicit trustees of a directory or file with just the rights needed for access.

# Universal AeroSpace File System Security

As described previously, the first step in planning file system security is to define the processing functions each user needs to perform. Table 6-3 shows file system use information Eric documented for each user in the Management, Engineer.ng, and Manufacturing departments.

Table 6-3 UAS file system use

| User | File System Use |
| :--- | :--- |
| All Users | Read files from the Forms directory<br>Run all applications except utility and CAD software<br>Read files in the Web directory<br>Rights to create and update files in the CORP\Shared and Temp directories |
| Management | Updates and maintains files in the CORP\Forms directory<br>Maintains the Management directory structure |
| Engineering Department | Creates and updates files in the Engineer\Shared directory<br>Reads files in the NASA and Aircraft directories<br>Runs CAD software |
| Kari Means (EngMgr Organizational Role) | Maintains the Engineer directory structure but should have only Read access to user home directory files<br>Also needs to be able to update engineering files in the Web directory |
| Lianne Jarka | Currently the lead engineer responsible for the Rover project (ISS), but this could change as additional engineers are moved on or off the project |
| Tony Rucci | Currently the lead engineer assigned to the ISS project, but as the needs for this project change, additional engineers might be moved on or off the project |
| Paul Aim | Senior engineer who works on all projects, so needs rights to Aircraft and NASA directories |
| Bradley Dah | Responsible for the Aircraft project |
| Manufacturing Department | Works with files in the Engineer\Shared directory<br>Needs Read, File Scan, and Write rights to the Inventory directory |
| Russ Pence (MfgMgr Organizational Role) | As head of the Manufacturing, Department, needs rights to maintain Requirements Planning System (RPS) and Manufacturing data |