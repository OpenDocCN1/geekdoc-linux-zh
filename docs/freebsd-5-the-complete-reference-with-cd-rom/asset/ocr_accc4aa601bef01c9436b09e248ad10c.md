![](bbox=[0.05, 0.1, 0.83, 0.44])

**Figure 2-13.** FreeBSD lets you enter critical account information for as many accounts as you’d like when you install the OS.

The Group field holds the user’s initial group—the group that will be assigned to files the user creates, used for programs the user runs, and so on. The Member Groups field holds the names of other groups to which the user belongs. The user will be able to access files that are accessible to these groups, and if the user creates a file in a directory owned by the group, that file will be accessible to members of the group. It’s possible you won’t need to enter anything in the Member Groups field, as shown in Figure 2-13.

> **Tip**
> The wheel group is one of the special groups maintained by FreeBSD. Members of this group may use the su command to acquire the privileges associated with another user, including root. When you create accounts for yourself and any other administrators of the computer, these users should belong to the wheel group, either via the Group field or the Member Groups field. Users who should not have such access should not belong to the wheel group.

If you’re unfamiliar with FreeBSD, you should leave the Home Directory and Login Shell fields at their default values. If you’re an experienced administrator, you may want to adjust these values.