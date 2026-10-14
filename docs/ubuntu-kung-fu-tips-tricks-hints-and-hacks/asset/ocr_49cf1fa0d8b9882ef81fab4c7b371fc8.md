# Understanding users

When you installed Ubuntu, a personal user account was created for you. As part of this process, a folder named after your username was created in `/home`, as mentioned previously.

# Root user

In fact, on most Linux systems two login accounts are created during installation—a standard user, and the root user. The root user is a special user account gifted with the ability to do anything, such as delete system files, or install software. Its username is always root.

Normally when Linux is used on a PC, a standard user logs into the root account whenever she has to administer the system, and then logs out when she’s finished. However, she will spend most of her time logged into her ordinary user account, doing day-to-day stuff like browsing the web.

Ubuntu differs slightly from most Linuxes. Although the root account is there in the background, the user is discouraged from directly logging in as root. Instead, the user “borrows” root powers to administer the system when necessary. Usually, this is done by simply entering your login password when prompted. See Figure 4-2 for an example that appears when attempting to run Synaptic, a program that administers software. Synaptic lives on the System ➞ Administration menu, and, in fact, if you run any program on this menu a password prompt dialog box will pop-up. You won’t be able to get any further until the password is typed but, after this, the application will run with root powers.

Alternatively, some applications will start, but will have restricted functionality until the UNLOCK button is clicked, at which point the same password request will appear. With these applications, typing your password doesn’t give the entire application root powers, but a component of it. This is more secure and, eventually, all of Ubuntu’s administrative applications will work this way.

> **NOTE**  
> When working at the command-line, any command needing administrative powers must be preceded by `sudo` (eg. `sudo sh` should be used for GUI apps). I explain more about this in Chapter 5.

# File permissions

Although the root user account has a back seat in Ubuntu, its influence is felt everywhere. Most operating system files are “owned” by the root user, and have permissions so that only root can edit them. In other words, only the root user—or a user borrowing root powers—can