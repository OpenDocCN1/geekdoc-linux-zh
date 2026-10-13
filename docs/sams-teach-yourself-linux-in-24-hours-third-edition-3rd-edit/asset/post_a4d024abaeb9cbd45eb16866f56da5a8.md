
2. Where do you find the list of window managers that are installed on your system?

Look in the /etc/X11/window-managers file. This file lists the name of the window manager, a brief description, the execution file, and the script needed to be able to access the window manager.

3. What is the easiest way to make changes to a file without losing the original information?

Use the comment-out character, the pound (#) sign. By using the comment-out character, if you need to return to the original values, you can delete the comment-out character. Another way to make changes without losing the original is to make a backup copy of the file before you begin editing. Then, if you make a mistake, you can always go back to the original by copying the copy back to the original filename.

4. Where is a good place to find more information about each of the window managers and desktop environments discussed during this chapter?

Visit the Web site. You might also find some useful documentation if you look around the Linux filesystem (try the /usr/doc directory).

## Exercises

1. You can use themes to dress up the desktop. Visit Themes.org (www.themes.org) and download a desktop theme for the window manager that you are using.

2. Experiment with some of the window managers discussed during the hour. If your system doesn’t have much RAM memory, you might want to try out one of the lightweight window managers, such as fvwm. Remember, it’s your desktop, so make it work for you.

![](img/782ecfdc0b083a767896cc983e10427f_308_0.png)

## PART V

## Network Administration

Hour

- 20 Talking to Users over a Network
- 21 Connecting to the Internet
- 22 Merging onto the Information Superhighway

![](img/782ecfdc0b083a767896cc983e10427f_310_0.png)

## Hour 20

## Talking to Users over a Network

Whether your Linux system is attached to a network or is used as a standalone machine, you can easily communicate with those people with whom you share computer resources. These methods don’t require an Internet connection or an Ethernet card; all you need to do is learn a few simple commands and edit a few files.

If your computer is attached to a network, you can easily find out which users are logged into the system and send them a message. The message appears on their terminal screens, and they can issue a single command to send a response back to you. This back-and-forth communication may sound similar to electronic mail. When you don’t have time to wait for a response, you can talk to other users using an interactive communication utility similar to Internet Relay Chat (IRC).

However, what do you do when your computer is not connected to a network but is shared by several people? Well, it’s time to call in a text editor and set up a bulletin board system. You can edit two files so that messages can be displayed on a login screen or after a user logs into his or her account.

In this hour, you will:

- List users who are logged in and how long their account has been active or idle
- Use the write and talk commands to communicate with other users on the system
- Change the login message and display a message of the day when users access their accounts

## Networking with Linux

The purpose of a computer network is to store and distribute data so that a group of people can share information easily and efficiently. When several people need to work together on a project, a network allows each person to work at his or her own computer and share files between members of the group. The group members can view the same file simultaneously, and even simultaneously add or delete data from a file, all without disturbing the work of the other users. Computer networking offers some real advantages. It reduces the amount of time and effort required to share a single file between several users and enhances communication between group members.

**New Term** A computer network is an interconnected assortment of computers, printers, hubs, cables, and other peripherals that store and manipulate data. A client/server network provides a connection to the server(s) that provide central repositories where users can store and retrieve files, and where users can share their data with other users. Microsoft Windows users might be familiar with the peer-to-peer networking concept in which machines may be connected by a cable and share messages and files without a server. Linux can be networked that way, but it already has facilities for a true client/server network that runs TCP/IP just like the Internet, and can be utilized through a browser in identical fashion.

Linux can be used in several ways to set up a computer network. The most common network configuration is the client/server network, shown in Figure 20.1. Most Linux networks use the client/server configuration, where a server controls the entire network and workstations are connected to the server through a network hub.

A client/server network is a good solution for the small business that needs to share information and computer hardware among several employees. Also, if you have more than one computer in your home and want to share files, printers, and Internet access, it may be time to take the network plunge. If you want to learn more about using Linux to set up a network, start with these Linux HOWTOs:

### FIGURE 20.1

This simple network accommodates four workstations (the clients) with one server.

![](img/782ecfdc0b083a767896cc983e10427f_312_0.png)

- The “Linux Networking Overview” HOWTO is the first place to start. This HOWTO provides an introduction to the networking capabilities of Linux, describes networking protocols (such as TCP/IP and PPP), and explains file and printer sharing.
- The “Linux Networking” HOWTO, which has until recently been known as the “Net-3” HOWTO, explains what you’ll need before you start building a network. In it you’ll find information about how you’ll configure network interface cards and what you need to know to set up the server.
- The “Ethernet” HOWTO lists the various Ethernet cards that are compatible with Linux and explains how you should configure them to work with the operating system. This HOWTO also discusses the different types of cable you can use to hook the network together.

A less common way to network your computer is by attaching one or more terminals to a computer, as shown in Figure 20.2. Using this configuration, a single computer controls more than one computer monitor through a serial port connection. A variety of terminals can be connected to a standalone computer this way—dumb terminals, text terminals, and graphics terminals. This is a very cost effective way of setting up a small network. For more information on how to connect terminals to a computer, check out the “Text Terminal” and “Serial” HOWTOs.

> A serial connection is not the only way to do this. You can also use a network card and category five Unshielded Twisted Pair (UTP) wiring.

![](img/782ecfdc0b083a767896cc983e10427f_313_0.png)

FIGURE 20.2
Attach several terminals to a computer through the serial port.

![](img/782ecfdc0b083a767896cc983e10427f_313_1.png)

## Locating Users on a Network

Because Linux is a multi-user, multitasking operating system, many people can share the resources of one computer. If the computer is attached to a network, there will be many users sharing the same network resources. If the computer is a standalone computer, several users can share the computer simultaneously using connected dumb terminals.

When all these people are logged into the system, how do you keep track of them all? An easy way to find out which users are logged into the system is with the who command. At a minimum, the who command will tell you which users are logged in. The terminals at which they're working, and how long each user has been logged in.

## Listing Users on the Network

When you only need to know which users are logged in, the terminals at which they are working, and the times that they logged in, simply type who at the shell prompt. Listing 20.1 shows the output of the who command when there are five users using the system.

### LISTING 20.1 Sample Output from the who Command

```
[rusty@localhost rusty]$ who
root      tty1   Jun 12 03:00
rusty     tty2   Jun 11 11:35
mona      tty3   Jun 11 12:09
dezi      tty4   Jun 11 11:36
lucy      tty5   Jun 11 11:36
```

Another way to find out who is using the network is with the finger command. The finger command displays the same information as the who command and adds the user's real name, how long the account has been idle, an office number, and a phone number. Listing 20.2 shows the logged-in users displayed by the finger command.

### LISTING 20.2 Sample Output from the finger Command

```
[rusty@localhost rusty]$ finger
Login Name    Tty Idle Login Time Office Office Phone
root  C Withers 1 05:53 Jun 12 03:00
rusty R Spoon   2     Jun 11 11:35
mona  M Rossman 3     Jun 11 12:09
dezi  D Forearm 4 22:57 Jun 11 11:36
lucy  L Amber   5 22:53 Jun 11 11:36
```

You may wonder where finger finds this extra information. The user's real name is displayed if the name is contained in the user's password file. The idle time is the amount of time that has passed since the user did anything with the account (such as type something at the keyboard or click the mouse).
