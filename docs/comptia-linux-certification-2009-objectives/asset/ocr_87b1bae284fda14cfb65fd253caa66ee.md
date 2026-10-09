+   2. Add user groups IT\_Support, Customer\_Support, Programming, and Design with the GID numbers specified.

+   a. Enter **groupadd -g 544 IT\_Support** to add a new group.

+   b. Enter **groupadd -g 545 Customer\_Support** to add the second group.

+   c. Enter **groupadd -g 546 Programming** to add the third group.

+   d. Enter **groupadd -g 547 Design** to add the fourth group.

+   3. Check that the users’ accounts and groups are created.

+   a. Enter **tail /etc/group** to view the group accounts on your system.

+   b. Observe that the newly added groups are displayed and have been added to the list of groups.

+   c. Observe that the user accounts have a default group created with the same name as the user.

+   d. Enter **tail /etc/passwd** to view the user accounts.

+   e. Observe that the newly added users are displayed and have been added to the list of users.

+   f. Enter **clear** to clear the terminal screen.