
## Configuring the X-Server

Assuming that you installed the X-Windows system, you are now asked if you want to configure the X-Server. Select Yes. You see a menu like the one shown in Figure 2.10.

![](img/48eec858cce7dfb89da36a4d40b7daf3_80_0.png)

**FIGURE 2.10** Selecting the X-Server configuration method.

In FreeBSD 5.0, one of the options available in this menu is xf86cfg. This is a graphical interface that helps you configure the X-Server. However, xf86cfg is a user interface night-mare, and it is easier to just configure the X-Server using the shell script prompts. Therefore, this section does not cover xf86cfg. Instead, go to Chapter 35, “Advanced X-Windows Configuration,” and read the section “Configuring X-Windows with the xf86config Script.” After you have finished with the xf86config script, return to this chapter and continue with the next section.

> **CAUTION**
>
> If you decide to try using xf86cfg anyway, you should be aware that improper refresh rate settings can cause damage to your monitor. Therefore, make sure you do not use settings your monitor is not capable of supporting. This is discussed in more detail in Chapter 35.

## Selecting the Default Desktop

Now you are back to the familiar text-based Sysinstall program, and you can no longer use the mouse. Instead, you must go back to using the arrow, Tab, spacebar, and Enter keys to navigate screens and choose options.

In the next screen, you can select which desktop you want to use as your default FreeBSD desktop in X-Windows. Unlike Microsoft Windows, FreeBSD allows you a wide choice of desktops with different features, looks, and so on. Far more desktops are available than are in this list, and they are very easy to change.

If you are an old Linux guru and you already know which desktop you want to use, select it here. If you have never worked with X-Windows before, I suggest you select the WindowMaker option because this desktop is fairly easy for new users to work with, and it is the one used in the next few chapters. If you later decide you don't like the desktop, you can always change it to a different one.

After you make your selection, the packages for your chosen desktop will be loaded onto your system.

## Installing Additional Software Packages

Select Yes to answer the question about whether you want to browse the FreeBSD package collection. From this menu, you can install some additional software that will be useful in the next couple chapters. Feel free to browse through the collection as long as you want, only to see what is available. For now, however, I don't recommend that you install a ton of software at this point because it is very easy to add more later. There are a few packages that I recommend you install for use in the next few chapters, however.

If you are asked where you want to install the packages from the Choosing Installation Media menu, select CDROM, assuming you are installing FreeBSD from the included CD-ROM.

Figure 2.11 shows the main menu for the package installation system.

![](img/48eec858cce7dfb89da36a4d40b7daf3_81_0.png)

**FIGURE 2.11** Installing additional packages.

To navigate through the package installation system, use the arrow keys to move between packages and categories. Use the spacebar or Enter key to select or unselect a package. When you have finished selecting packages in a category, use the Tab key to highlight the OK option and press Enter to get back to the main selection menu (where you can select the category you want to browse). Packages that are already installed will have an X next to them; unselecting these packages causes them to be uninstalled. Packages that have a D by them are dependencies, meaning that they are required by some other package currently installed. At the bottom of the screen is a short description of the currently highlighted package.

> **NOTE**
>
> By the time this book goes to press, some of the version numbers on the software listed may have changed. In this case, select the option that appears closest to what I list here. For example, I list Bash-2.05. If your menu has Bash-2.07 instead, select it.

I suggest that you choose the Bash-2.05 package in the Shells category. This is a very powerful and easy-to-use shell for the FreeBSD command-line interface. Linux users will be familiar with this shell because it is the default shell on almost all Linux distributions.

Unix gurus can also install any other shell in this list that they want to have available.

## Adding a User

When the package installation is complete, you are asked whether you want to add any user accounts to the system. Select Yes to create a normal user account for yourself. It is dangerous to use the root account for normal operations because root has no restrictions and can damage or destroy important system files if you make a mistake. Using your normal user account for most operations prevents this.

On the Help screen, shown in Figure 2.12, select User to add a new user to the system.

![](img/48eec858cce7dfb89da36a4d40b7daf3_82_0.png)

You are then taken to a form you need to fill out to add the new user (see Figure 2.13).

![](img/48eec858cce7dfb89da36a4d40b7daf3_82_1.png)

Not all the fields on this form have to be filled in. Actually, you should leave some of them blank so the system can make a default choice for you. Use the Tab key to move between the various fields. The following sections describe each of these fields and make recommendations for adding values to them.

### Login ID

Login ID is the name you use to identify yourself to the system when you sign in. The ID you type in this field should not be more than eight characters long. Common conventions are to use initials, nicknames, or combinations of initials and first or last name. For example, I might use `mikeu`, `murban`, or `meu` as my login name. Each user on the system must have a unique login name. Names are case sensitive and, by convention, use all lowercase letters.

### UID

UID is a numeric ID that the system uses to keep track of users. You should leave this field alone and let the system pick the number for you.

### Group

This field refers to the primary group you will be a member of. Once again, leave this field alone and let the system pick for you.

### Password

In this field, you type the password you will use to log in. Passwords are case sensitive. Here are some guidelines for choosing good passwords that crackers (commonly known as *hackers*, although this is not the correct term for people who illegally break into computer systems) can’t figure out:

- Use at least eight characters. Short passwords are easier for programs designed to try random combinations of letters and numbers to crack.
- Use a combination of uppercase and lowercase letters, numbers, and at least one special character, such as $ or !.
- Don’t use words found in a dictionary. Password-cracking programs exist that go through the dictionary trying various words until they hit one that works.
- Don’t use things that other people know about you or can easily find out about you. In other words, the name of your child, your cat, or the city you were born in does not make a good password.

At the same time, it’s good to pick something you can remember easily. Some techniques for doing this include combining parts of various words together (remembering, of course, to include both uppercase and lowercase letters and to stick a few numbers and at least one special character in somewhere). You can also use what I call *keyboard substitution*—a technique where you pick a word that means something to you (but that others will not know) and then substitute the character to the upper-left, upper-right, lower-left, or lower-right as the actual character in the password.

After you decide on a password, enter it carefully because you will not be asked to verify it. (The password will show up on the screen as asterisks (*). If you mistype it, you will not be able to log in (if you accidentally do mistype the password, you can read how to fix it in Appendix C).)

After you decide on your password, do not write it down anywhere. Do not write it on the bottom of your desk. Do not write it down in your appointment book. Do not have it tattooed on your arm. And whatever you do, do not write it on a Post-It note and stick it on your monitor. (I know that seems like stating the obvious, but you would be surprised how many users do just that.) Also, do not tell your password to anybody, including your coworkers, your spouse, or your children.

### Full Name

You can either type your name in this field or leave it blank (remove “User &” if you intend to leave it blank). Note that some programs, such as the Unix **mail** program, will use this field to determine what to put in the From field of the e-mail you send. Therefore, it is probably a good idea to enter your name here.

### Member Groups

I suggest you type **wheel** in this field. This will make you a member of the group “wheel,” which will allow you to assume the identity of the root user (super-user or system administrator) without having to log out and log back in as a different user (although you still need to supply the root password to do this).

### Home Directory

This field lists the place where your home directory will be located on the hard disk. You should leave this field alone and let the system choose for you.

### Login Shell

The login shell is the default command-line shell you will be placed in after you log in. Assuming you installed the Bash shell, as suggested earlier, I suggest you type /usr/local/bin/bash in this field (including the slashes). If you later decide you do not like the Bash shell, it is easy to change your default shell to a different one.

After you finish entering the information, tab over to the OK button and press Enter. The user account will be created for you, and you will be returned to the menu shown earlier in Figure 2.12. Select the Exit option.

## Setting the Root Password

Press Enter when you see the message about setting the system manager's password. You are then given a prompt at the bottom of the screen that asks you to enter a root password. It looks like this:
