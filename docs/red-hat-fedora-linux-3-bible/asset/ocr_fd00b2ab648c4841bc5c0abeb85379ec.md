# Chapter 11: Setting Up and Supporting Users  417

![](bbox=[0.25, 0.08, 0.62, 0.35])

Figure 11-2: The Create New User window

+   2. Type the requested information in the following fields:

+   - **User Name** —— A single word to describe the user. Typically, the user name is eight characters, all lowercase, containing the user’s real first name, last name, or (more often) a combination of the two (such as `jwones`).

+   - **Full Name** - The user’s full name (usually first name, middle initial, and last name). This name is typically just used for display, so using upper- and lowercase is fine.

+   - **Password** — The user’s initial password. (Ask the user to change this password the first time he or she logs in to the new account, using the `passwd` command.)

+   - **Confirm Password** — Type the password again, to make sure you entered it correctly.

+   - **Login Shell** — The default shell (for entering typed commands) that the user sees when first logging in to Fedora from a character display.

+   - **Create home directory** — By default, this box is selected and the user’s home directory (as indicated by the Home Directory field) is created automatically.

+   - **Home Directory** - By default, the user is given a home directory of the user’s name in the /home directory. (For example, the user `sheeee` would be assigned `/home/sheeee` as her home directory.) Change this field if you want to assign the user to a different home directory.

+   - **Create a private group for the user** —Check this box if you want a group by the same name as the user, created for this user. The name is added to the /etc/group file. This feature is referred to as user private groups (UPGs).

```
**TIP:** Using UPGs can be a benefit for sharing a directory of files among several users. Here’s an example:
# useradd -m projectx
```