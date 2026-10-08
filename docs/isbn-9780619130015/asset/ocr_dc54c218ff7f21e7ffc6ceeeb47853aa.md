# The Ordinary User's Command Line

The $ (dollar sign) is traditionally associated with ordinary users. The UNIX system generates a default setting for the command prompt for ordinary users. The following format is common on Linux systems:

[ user name@hostname ]$

In the prompt, *user name* is the user's login name, such as *jean*, and *hostname* is the name of the computer the user is logged on to.

# Changing Passwords

Your user name, or login name, identifies you to the system. You may choose your own user name and give it to the system administrator, who then adds you as a new user. As mentioned before, UNIX recognizes up to eight characters in your user name, which is often your first name or nickname. The user name is unique, but not confidential, and may be provided to other users. The password, on the other hand, is confidential and secures your work on the system. You can change your password, if necessary, by using the passwd command. If you do not have a password, use the passwd command to create one.

UNIX lets you change your password only if the new one differs from the old password by at least three characters; the password has more than five characters, including at least two letters and one number; and the password is different from your user name.

The password you chose for the Dominion system—Gscott956—is too similar to another password on the system, so the system administrator asks you to change it.

To change your password:

+   1.  Type **passwd** after the command prompt, and press **Enter**.
2.  Type your new password and press **Enter**. Your new password does not appear on the screen as you type.
3.  Retype your new password and press **Enter** so that UNIX can confirm the new password.

help

If the password you retype as confirmation does not match your new UNIX password, UNIX asks you to enter the password again. UNIX may also ask you to choose a different password because you chose one that is too short or too easily guessed, such as *password*.

After changing your password, you should log out and log on again to make sure UNIX recognizes your new password.