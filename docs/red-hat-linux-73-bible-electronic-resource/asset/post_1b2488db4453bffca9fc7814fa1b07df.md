
# Part II

# Using Red Hat Linux

- Chapter 3: Getting to Know Red Hat Linux
- Chapter 4: Working with the Desktop
- Chapter 5: Accessing and Running Applications
- Chapter 6: Publishing with Red Hat Linux
- Chapter 7: Playing Games with Red Hat Linux
- Chapter 8: Multimedia in Red Hat Linux
- Chapter 9: Tools for Using the Internet and the Web

## Chapter 3
### Getting to Know Red Hat Linux

#### In This Chapter

- Logging in to Red Hat Linux
- Understanding the Red Hat Linux shell
- Using the Red Hat Linux shell
- Working with the Red Hat Linux file system
- Using the vi text editor in Red Hat Linux

This chapter presents a view of Red Hat Linux from the shell. The shell is a command-line interpreter that lets you access some of the most critical Red Hat Linux tools. The shell is powerful, complex, and almost completely unintuitive.

Although, at first, it isn't obvious how to use the shell, with the right help you can quickly learn many of the most important shell features. This chapter is your guide to logging in and working with the Linux system commands, processes, and file system from the shell. After describing the simple process of logging in to Red Hat Linux, this chapter describes the shell environment and helps you tailor it to your needs. It also describes how to use and move around the file system.

### Logging in to Red Hat Linux

Because Red Hat Linux was created as a multiuser computer system, even if you are the only person using the computer, you start by logging in. Logging in identifies you as a particular user. With that identity, Red Hat Linux can start up your configuration and give you appropriate permissions to files and programs.

After the computer has been turned on and the operating system has started, you see either a graphical login screen (default) or a text-based login prompt. The text-based prompt should look similar to this:

```
Red Hat Linux release 7.3
Kernel 2.4.18-0.1 on an i686

localhost login:
```

The graphical login is typically your entry into the X Window System graphical user interface (GUI). Figure 3-1 is an example of the login window you see if you are using the Gnome desktop environment.

![](img/1744bde8c889adfab3fc911e1687fecf_97_0.png)

**Figure 3-1:** A graphical login can access the Red Hat Linux GUI.

Notice the several menu buttons on the login screen. You can ignore them and simply log in. Or you can use these buttons as follows:

- **Session** — Usually when you log in, your graphical desktop starts up (either Gnome or KDE desktops). Click **Session** to choose a different desktop (if available) or to select Failsafe. If you can’t remember which desktop to use, you can choose **Last** (to use the desktop you used most recently) or **Default** (to use the desktop set as your default). You use Failsafe if you want only a shell interface (the shell is described later in this chapter).

> **NOTE:** The failsafe session is used primarily to correct problems when, for some reason, your desktop session won’t start properly. For example, graphics settings may be wrong, resulting in a garbled screen. The failsafe session simply opens a shell window so you can type commands to correct the problem before you log in again. When you are done with a failsafe session, type `exit` to be allowed to log in again.

- **Language** — Click **Language** to select a language other than the last language you used (indicated by the **Last** button on this menu). (You need additional software packages to use different languages.)

- **System** — If instead of logging in, you want to shut down or restart the computer, click **System**, and select either **Reboot** or **Halt**.

For a normal login, at the login prompt type your user name and, when prompted, your password. Every Linux system has a *root* user and at least one non-root user (with a name of your choosing) assigned when Linux is installed. The root user has the capability to run programs, use files, and change the computer setup in any way. Because the root user has special powers, and can therefore do special damage, you usually log in as a regular user (which only has access to that user’s own files and those that are open to everyone).

As someone just using the Linux system, you probably have your own unique user name and password. Often that name is associated with your real name (such as jobh, susanp, or dave4). If you are still not sure why you need a user login, see the sidebar “Why Do I Need a User Login?” for more information.

> **CROSS-REFERENCE:** See Chapter 10 for a description of the root user and Chapter 11 for information on how to set up and use other user accounts. Refer to Chapter 14 for suggestions on how to choose a good password.

#### Why Do I Need a User Login?

If you are accustomed to using a PC, and you are the only one using your Linux computer, you may wonder why you need a user account and password. Unlike Windows, Linux (as its predecessor UNIX) was designed from the ground up to be a multiuser system. Here are several good reasons why you should use separate user accounts:

- Even as the only person using a Linux system, you will want a user name besides the root user for running applications and working with files to prevent you from changing critical system files by mistake during your everyday computer use.
- If several people are using a Linux system, separate user accounts let you protect your files from being accessed or changed by others.
- Networking is probably the best reason for using a Linux system. If you are on a network, a unique user name is useful in many ways. Your user name can be associated with resources on other computers: file systems, application programs, and mailboxes to name a few. Often a root user is not allowed to share resources on remote Linux systems.
- Over time, you will probably change personal configuration information associated with your account. For example, you may add aliases, create your own utility programs, or set properties for the applications you use. By gathering this information in one place, it's easy to move your account or add a new account to another computer in the future.

#### The login session

As you log in, Red Hat Linux starts up a user environment that is unique to your user account. Various attributes are set that remain active during your login session until they are changed. Some of the features that make up your user environment are:

- **A home directory** — The home directory identifies a location on the computer's hard disk where you can save and protect the files that you need. You can organize your files any way you like and assign permissions to those files to prevent or allow access to them by others.

The root user’s home directory in Linux is usually /root. Other users typically have home directories in the /home directory. For example, if your user name were johnq, your home directory would probably be /home/johnq.

- **A shell configuration** — There are several shells available for use with Linux, with each having slightly different features. The *bash* shell (which stands for Bourne Again Shell) is most commonly used with Linux. (In this chapter, *bash* is used to show how to work with the shell.)

Within your home directory are several configuration files that set up properties for your shell login session. These files may identify the path (where programs are located that you can use), contain environment variables and aliases (described later), and define functions that make your work more efficient.

> **NOTE:** Configuration files usually begin with a dot (.), so they do not appear by default when you list the contents of the directory (type `ls -a` to see dot files). Examples of these files and descriptions of how to configure them are discussed later in this chapter.

- **A graphical configuration** — If you are set up to use Linux through a GUI, there are many ways you can configure how that GUI behaves. Most GUIs used with Linux are based on the X Window System (often referred to simply as X). While X provides a framework for a GUI that lets you run applications, it enables you to choose from many different *desktop environments*. For Red Hat Linux, the Gnome and KDE desktop environments are available to provide a cohesive interface to the applications, menus, and windows of your GUI. Different *window managers* can be used as well, to provide a specific look and feel of the GUI. (Window managers can define the colors, fonts, mouse behavior, window controls, menus, and other surface features of your desktop.)

Besides choosing a desktop environment, you can set up your own desktop properties. These properties can change such things as colors, locations of icons, application menus, and other attributes to make your GUI efficient and, if you like, attractive to the eye.

When the login process is complete, either a shell or a GUI is started automatically. This chapter goes into detail about how to use the shell.

> **CROSS-REFERENCE:** Chapter 4 describes how to use the Gnome and KDE desktop environments, as well as the X Window System itself.

#### The shell interface

If your Red Hat Linux system has no GUI (or one that isn’t working at the moment), you must enter commands from the shell. If you are using a shell interface, the first thing you see is the shell prompt. The default prompt for a user is simply a dollar sign:

```
$
```

The default prompt for the root user is a pound sign (also called a hash sign):
