# Part I: Getting Started with Ubuntu

# FIGURE 2-14

Selecting an operating system on a dual-boot x86 system

![](bbox=[0.108, 0.176, 0.593, 0.445])

# The First Time You Boot Ubuntu

The first time you boot Ubuntu, you will want to update your system. This ensures that you have the latest and best versions of all of the standard Ubuntu software, which provides security-related fixes, bug fixes, and general enhancements. After any first-time boot screens (discussed in the remainder of this section), the Ubuntu Update Manager will run automatically and display an icon alerting that updates are available in the top-right portion of the panel on an Ubuntu system, or a dialog to the same effect on your main screen. For information about updating an Ubuntu system, see the section of Chapter 19, "Adding, Removing, and Updating Software," or "Using the Ubuntu Update Manager."

If you selected the "Require my password to log in and decrypt your home folder" option on the screen shown in Figure 2-11 when you were installing Ubuntu, you will see an information dialog about recording your encryption passphrase. This dialog offers to run an application that enables you to specify a passphrase as a backup mechanism for you to decrypt your home directory. Ubuntu's automatic directory encryption mechanism normally uses your password to decrypt an encrypted directory, but also supports a passphrase as an alternate decryption-mechanism. When this dialog displays, click "Run this now" to proceed.

A standard terminal window opens, displaying a "Passphrase." prompt. Enter a word or series of words that you will remember, and press Return. The information dialog re-displays, at which point you can click Close to terminate that dialog and begin using your new Ubuntu system. If you want to change the passphrase for your encrypted directory, you can use the encryptfs-unwrap-passphrase command from the command line to do so.

46