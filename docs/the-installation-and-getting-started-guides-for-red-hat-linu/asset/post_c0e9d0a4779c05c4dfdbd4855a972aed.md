
## Deleting a Group — General Overview

To delete a group:

- Start Linuxconf by typing linuxconf at the shell prompt.
- Open [Config] -> [Users accounts] -> [Normal] -> [Group definitions].

If you have more than 15 groups, you will be given a filter screen (see figure 8-9) to narrow your choice of groups by specifying a prefix.

- With or without a prefix select Accept at the bottom of the screen.
- On the User groups screen (see figure 8-10) select the group you wish to delete.
- You'll be presented with the Group specification screen (see figure 8-11).
- Select Del to delete the group. Linuxconf will then prompt you to confirm the deletion. Choose yes to delete the group.

The group's files will still remain and their respective owners will still have sole control over them. The group name will be replaced with the deleted group's ID. The files may be assigned to a new group by using the chgrp command. More information on chgrp can be found by typing the command info chgrp or man chgrp at the shell prompt. If a new group is created and the deleted group's ID is specified then the new group will have access to the deleted group's files. Don't worry, Linuxconf doesn't recycle old group numbers any more than it does old user IDs, so it won't happen by accident.

## Modifying Group Membership

There are two ways to modify the list of users that belong to a group. You can either update each user account itself, or you can update the group definitions. In general, the fastest way is to update each of the group definitions. If you're planning on changing more information for each user than just the group information, then updating each user account may prove easier.

## Modifying Group Membership — Quick Reference

### Under Groups

- 1 Start Linuxconf by typing linuxconf at the shell prompt.
- 2 Open [Config] -> [Users accounts] -> [Normal] -> [Group definitions].
- 3 Select the group to which you wish to add or remove users.
- 4 Add or remove new users to the Alternate members(opt) field; make sure all user names are separated with a space " " character.
- 5 Select Accept.

### Under Users

- 1 Start Linuxconf by typing linuxconf at the shell prompt.
- 2 Open [Config] -> [Users accounts] -> [Normal] -> [User accounts].
- 3 Select a user to which you wish to add or remove groups. Adjust the Supplementary groups field accordingly; make sure all the group names are separated with a space " " character.
- 4 Select Accept.
- 5 Repeat steps 3 through 5 for each additional user to be added.

## Modifying Group Membership — General Overview

We'll start by detailing the group definitions method.

- Start Linuxconf by typing linuxconf at the shell prompt.
- Open [Config] -> [Users accounts] -> [Normal] -> [Group definitions].

If you have more than 15 groups, you will be given a filter screen (see figure 8-9) to narrow your choice of groups by specifying a prefix.

- With or without a prefix, select Accept at the bottom of the screen.
- Select the group you wish to modify. This will open the Group specification screen (see figure 8-11).
- Add or remove each user from the Alternate members field. Make sure that all of the user names are separated by a space " " character.
- Once you've done this select Accept which can be found at the bottom of the screen.

This will automatically update each user account with the group showing up in the Supplementary groups field if added or absent if removed. Adding and removing groups can also be done by modifying each individual user account.

- Start Linuxconf by typing linuxconf at the shell prompt.
- Open [Config] -> [Users accounts] -> [Normal] -> [User accounts].

If you have more than 15 accounts on the system, Linuxconf will provide you with a filter screen (see figure 8-2).

- On the User accounts screen (see figure 8-3), select a user that you wish to update. You will be presented with the User information screen (see figure 8-6).
- Add or remove the desired groups from the Supplementary groups field. Each group should be separated by a space " " character.
- Once you've made all the changes you'd like, select Accept at the bottom of the screen.

This will automatically update the group definitions. Repeat the process for each user.

## CD-ROMs, Diskettes, Hard Drives and Filesystems — the Inside Track

A filesystem is composed of files and directories, all starting from a single root directory. The root directory may contain any number of files and other directories, with each directory in turn following suit. The average filesystem often looks like an inverted tree with the directories as branches and the files as leaves. Filesystems reside on mass storage devices such as diskette drives, hard drives, and CD-ROMs.
