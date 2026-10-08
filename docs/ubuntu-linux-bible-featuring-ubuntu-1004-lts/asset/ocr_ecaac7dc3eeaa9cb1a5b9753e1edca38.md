# Part III: Ubuntu for System Administrators

Enter the name of the new group that you want to create in the Group name box. Next, you can optionally modify the group number associated with this group.

At this point, you can also add selected users to the group that you are creating by clicking the checkbox to the left of their names in the Group members list. If you change your mind about adding a specific user to your new group, simply deselect the checkbox beside their name in the Group members list.

Once you are finished changing settings and adding members to your new group, click OK to create that group and return to the Groups settings dialog of the Users and Groups application. If you are finishing creation or modifying groups, you can click Close to exit the Groups settings dialog and return to the Users Settings dialog. To completely exit the Users and Groups application dialog, click Close on the Users Settings dialog.

# Managing Existing Groups

In addition to simplifying the creation of new groups, the Users and Groups tool also simplifies adding and removing users from those groups. To update groups' memberships, start the Users and Groups tool by selecting the System Administration -> Users and Groups menu to execute this tool. The dialog shown in Figure 27-1 allows. To access the group-oriented portions of this tool, click the Manage Groups button to display the dialog shown in Figure 27-5.

In this dialog, click the name of the group that you want to add or remove users from, and click Properties. This displays a dialog that is essentially identical to the dialog shown in Figure 27-6 except that you cannot change the name of the group, only its members or group ID.

# Tip

You should rarely, if ever, use the Group settings dialog to change group IDs. Changing the group ID in this dialog changes the entry for the group in the file /etc/passwd but does not change the group ID of any files that may happen to be already owned by that group. This could prevent any per-group protections that are already in working correctly, preventing users that be authorized from accessing files or directories associated with their group. ■

To add a user to an existing group, click the checkbox to the left of that user's username in the scrollable list at the bottom of this dialog. Similarly, to remove a user from an existing group, deselect the checkbox beside that user's username in the scrollable list of Group Members.

Any membership, name, or group ID changes that you make in this dialog are not written to the /etc/passwd file (if updated in the /etc/passwd if necessary) until you click OK. You can click Cancel at any time to discard your changes. Clicking either of these buttons returns you to the Groups settings dialog. Once you have finished making any changes to group memberships or other properties, click OK to close the Groups settings dialog and return to the Users Settings dialog. To completely exit the Users and Groups tool, click Close.