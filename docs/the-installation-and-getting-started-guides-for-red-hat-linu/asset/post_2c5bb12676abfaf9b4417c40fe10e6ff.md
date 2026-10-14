
## Finalizing Printer Setup

Next, you'll see a dialog box entitled “Configure Printer” (see Figure 6-13). Select the printer type that most closely matches your printer. Select Next, and press [Space] to continue.

![](img/46f4935125ba89e12897afbe9d77a097_148_0.png)

Figure 6-13: Configure Printer

After selecting the printer type, you will see a dialog box similar to the one in Figure 6-14. Set the paper size and resolution appropriately. The Fix stair-stepping of text check box should be checked if your printer does not automatically perform a carriage return after each line.

![](img/46f4935125ba89e12897afbe9d77a097_149_0.png)

### Figure 6-14: Printer Settings

If your printer supports it, you will see a dialog box in which you can configure the color options of your printer, or a similar one, in which you can configure the color and resolutions options of the uniprint driver your printer uses. Set these options appropriately.

Finally, you'll see a dialog box that contains all the information pertaining to your printer (see Figure 6-15). Verify that the information is correct. If everything looks OK, select Done. If you need to make changes, select Edit. You can also select Cancel if you'd rather not configure a printer at this time.

![](img/46f4935125ba89e12897afbe9d77a097_150_0.png)

### Figure 6-15: Verifying Printer Information

If you select Done, you will be given the option to configure another printer, or you may continue with the installation.

## Setting a Root Password

The installation program will next prompt you to set a root password for your system (see Figure 6-16). You'll use the root password to log into your Red Hat Linux system for the first time.

![](img/46f4935125ba89e12897afbe9d77a097_151_0.png)

Figure 6-16: Root Password

The root password must be at least six characters long; the password you type is not echoed to the screen. You must enter the password twice; if the two passwords do not match, the installation program will ask you to enter them again.

You ought to make the root password something you can remember, but not something that is easy for someone else to guess. Your name, your phone number, qwerty, password, root, 123456, and anteater are all examples of poor passwords. Good passwords mix numerals with upper and lower case letters and do not contain dictionary words: Aard387vark or 420BMttNT, for example. Remember that the password is case-sensitive. Write down this password and keep it in a secure place.

**Please Note:** The root user (also known as the superuser) has complete access to the entire system; for this reason, logging in as the root user is best done only to perform system maintenance or administration. Please see Chapter 8 for instructions on how to add a user account for yourself after you reboot your system. A more basic method of creating a new user account can also be found in the Red Hat Linux Getting Started Guide in the Welcome to Linux chapter.

## Authentication Configuration

After you have set up your root password, you will have the option of setting up different network password authentications:

- **Enable NIS** — allows you to run a group of computers in the same Network Information Service domain with a common password and group file. There are two options here to choose from:
  - ✓ **NIS Domain** — this option allows you to specify which domain or group of computers your system will belong to.
  - ✓ **NIS Server** — this option causes your computer to use a specific NIS server, rather than "broadcasting" a message to the local area network asking for any available server to host your system.

- **Enable Shadow Passwords** — provides a very secure method of retaining passwords for you. The /etc/passwd file is replaced by /etc/shadow which is only readable by root.

- **MD5 Password** — allows a long password to use up to 256 characters, instead of the standard eight letters or less.

**Please Note:** To configure the NIS option, you must be connected to an NIS network. If you are unsure whether or not you are connected to an NIS network, please ask you system administrator. Unless you are setting up a NIS password, you will notice that both Shadow password and MD5 are selected. We recommend you use both to make your machine as secure as possible (see Figure 6-17).
