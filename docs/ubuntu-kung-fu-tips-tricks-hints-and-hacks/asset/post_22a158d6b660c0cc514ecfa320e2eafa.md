
## Understanding users

When you installed Ubuntu, a personal user account was created for you. As part of this process, a folder named after your username was created in `/home`, as mentioned previously.

## Root user

In fact, on most Linux systems two login accounts are created during installation—a standard user, and the root user. The root user is a special user account gifted with the ability to do anything, such as delete system files, or install software. Its username is always root.

Normally when Linux is used on a PC, a standard user logs into the root account whenever she has to administer the system, and then logs out when she’s finished. However, she will spend most of her time logged into her ordinary user account, doing day-to-day stuff like browsing the web.

Ubuntu differs slightly from most Linuxes. Although the root account is there in the background, the user is discouraged from directly logging in as root. Instead, the user “borrows” root powers to administer the system when necessary. Usually, this is done by simply entering your login password when prompted. See Figure 4-2 for an example that appears when attempting to run Synaptic, a program that administers software. Synaptic lives on the System ➞ Administration menu, and, in fact, if you run any program on this menu a password prompt dialog box will pop-up. You won’t be able to get any further until the password is typed but, after this, the application will run with root powers.

Alternatively, some applications will start, but will have restricted functionality until the UNLOCK button is clicked, at which point the same password request will appear. With these applications, typing your password doesn’t give the entire application root powers, but a component of it. This is more secure and, eventually, all of Ubuntu’s administrative applications will work this way.

> **NOTE**  
> When working at the command-line, any command needing administrative powers must be preceded by `sudo` (eg. `sudo sh` should be used for GUI apps). I explain more about this in Chapter 5.

## File permissions

Although the root user account has a back seat in Ubuntu, its influence is felt everywhere. Most operating system files are “owned” by the root user, and have permissions so that only root can edit them. In other words, only the root user—or a user borrowing root powers—can

![](img/48d064407ff591f0b5365c2d2919ee6e_72_0.png)

Figure 4-2. Typing a password to borrow root powers and administer the system.

delete or modify vital files. In some cases, even viewing operating system files by ordinary users is prohibited.

This simple mechanism of protecting operating system files through root user ownership is how Linux enforces security and system protection. It's simple but highly effective, and has stood the test of time for many years.

> NOTE The fact that Windows fails to make this distinction, and effectively merges the standard and administrator types of user account, is one reason it's so insecure. If a virus infects the system, it operates with administrator powers, so it is really cause trouble. Vista fixes this situation somewhat by pestering the user every time they do something even remotely dangerous to the system.

File permissions lie at the heart of understanding and working with the Linux filesystem, so let's take a look at them in more depth.

As mentioned previously, every file is owned by a particular user—even system files, which are owned by the root user.

The owner of a file can set three separate sets of permissions: firstly for himself, secondly for the group, and lastly for all others.

In setting file permissions for himself, the file's owner could mark a file as read-only, for example, to avoid accidentally changing it.

All users are members of a group, and each file is assigned to a particular group, in addition to being owned by a user. So, a separate set of file permissions can be granted for members of that group.

A third and final set of permissions can be configured for others, which is to say, users on the computer who aren't the file's owner, and who aren't in the group.
