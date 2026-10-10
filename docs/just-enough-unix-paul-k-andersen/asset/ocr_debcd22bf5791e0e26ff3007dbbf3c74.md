# 21.9 Making a calendar File

The `calendar` utility will remind you of upcoming events. This requires that you have a `calendar` file in your home directory, and that you modify `.profile` to read the `calendar` file.

+   1.  **Edit your `.profile` with the text editor.** Add the following line:
+       `calendar`
+   2.  **Write the change into the file and quit the editor.**
+   3.  **Use the text editor to create a `calendar` file.** Be sure to use this exact spelling of `calendar`, in lowercase letters. Otherwise, the shell won't recognize the file.
+   4.  **Add a message to the `calendar` file.** Include today’s date in the message:
+       `This is a test for [today’s date]`
+   5.  **Write the changes into the `calendar` file and quit the editor.**
+   6.  **Use the “dot” command to run the `.profile` file.**
+       `/home/you > . .profile` `(Return)`
+       You should see your login message, the message about your terminal type, and the `calendar` message:
+       `Your wish is my command, Oh Great One.`
+       `Terminal set to vt100`
+       `This is a test for [today’s date]`

*Write the date in the form Apr 12, Apr 12, or 4/12.*

# 21.10 Creating a .kshrc File (ksh only)

If you are a `ksh` user, you may create a shell initialization file named `.kshrc`. This file is typically used for setting up command aliases and the `history` mechanism. Before doing this, however, you need to edit `.profile`:

+   1.  **Use the text editor to edit `.profile`.** Add the following lines to the file:
+       ```
+       ENV=$HOME/.kshrc
+       export ENV
+       ```
+       This tells `ksh` that it should look for `.kshrc` in your home directory. If the `ENV` variable is not set, `ksh` will not execute `.kshrc`.
+   2.  **Write and quit the editor.**
+   3.  **Use the text editor to edit the `.kshrc` file.** Start by inserting a comment line, giving today’s date: