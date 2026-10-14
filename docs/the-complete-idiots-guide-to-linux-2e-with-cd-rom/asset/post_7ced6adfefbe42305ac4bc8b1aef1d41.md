
![](img/edf072a03d4de1f8f4a13465ac79e7fb_101_0.png)

Messenger’s Compose Window—this is where you type a new email message.

Kmail is very similar in interface to Netscape’s Messenger component. However, at the moment, Messenger is a more polished product with better tools and features.

## News

If you have time to wander through Usenet, no doubt you will find a lot of useful and useless stuff. If you want to surf, you’ll need a decent news reader. Again, the choices for you are several: under KDE you have knews, and under any X-Windows, including KDE, you have Netscape’s Collabra.

> Techno Talk: What Is Usenet?
> Usenet is a worldwide distributed discussion system. It is made up of a classified hierarchy of topics grouped by subject (newsgroups). Messages are broadcast and propagated between news servers. Some groups are moderated, meaning that information posted by users needs to be approved prior to posting. Others are not moderated.
> 
> For a detailed description of what Usenet is and is not, see http://www.cis.ohio-state.edu/hypertext/faq/usenet/usenet/what-is/part1/faq.html

Collabra doesn’t make too much of a distinction between email and news. Although the configuration to access them is different, the result is similar. You use Collabra to subscribe to newsgroups that interest you, and then you use Messenger to read and post messages. Before you can read news, however, you need to download a list of what messages are available. When you click on one of them, the message is then downloaded and you can view it. If you want to post a message, you compose one basically like you compose an email message, but instead it is posted to a news server. From there the message is disseminated around the globe.

Configuring your system to use news is simple: You connect to a news server (nntp server; the name of this machine is provided by your ISP), and you download a very long and large list of newsgroups available from that server. (There are thousands and thousands of different groups.) You then select all the groups that interest you and start reading (see the next three figures). As a sanity check, you might want to assign an amount of time per day that you want to do this. It’s very easy to get caught up in news reading and not realize that hours have flown by. As a choice, I tend not to look at newsgroups unless I am searching for specific information. Several years ago, I used to spend more than anyone’s share reading news. Today I try to stay away; it’s easy to get caught up in the noise.

If your ISP serves news under a special port, enter in the Port space; otherwise leave the default 119. Organizations also use news to distribute information. Some of these newsgroups are only available through a secure server that

requires authentication: if your news server requires this, check the Secure checkbox next to the Port space.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_102_0.png)

The news configuration panel. To configure your news, use the Preferences command under the Edit menu in any Communicator window.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_102_1.png)

After you define your news server, you’ll be presented with this window. Here, you can select the groups to join from those carried by your news server.

If you know the name of a newsgroup that interests you, type it next to Discussion Group and click Join.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_102_2.png)

Messenger displaying a list of newsgroups.

Use the Reply button to reply to a posting. If you hold it down, a menu will allow you to choose the reply method: to the group, to the poster, or to a combination of the two. A posting listed in bold indicates it hasn’t been read yet.

## Telnet

Telnet is an additional way to interact with another computer on the Internet. It is a command line only program that allows you to access a remote UNIX-like computer through a command line interface. Telnet is discussed in Chapter 17, “Command Toolbox: Useful Shell Commands and Shortcuts.”

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Chapter 10
Customizing KDE

## In This Chapter

- Adding an Application to the Panel or Application Launcher
- Other KDE Options
- The KDE Control Center

KDE is fairly customizable; here’s a quick guide on what you can do to customize your desktop. Most of KDE is customized through the use of kdelnk files (files that have a kdelnk extension). These files provide configuration information that KDE uses to associate files with applications, icons with applications and documents, devices such as disk drives with icons (see Chapter 7, “Working with Disks”), and others.

The KDE Panel can be customized in several ways. The following sections present some of the most useful.

## Adding an Application to the Panel or Application Launcher

Adding an application to the panel is a simple two-step process. First, you’ll need to create a kdelnk file that provides information about the application you want. This file will associate an executable program with an icon and its files. Then you install the kdelnk file by dragging it into the panel or putting it in a

special directory where the application launcher will find it.

### Creating a Kdelnk File that Represents an Application

Creating a .kdelnk file for an application is easy. The process is very similar to the process we used to create a .kdelnk file for your floppy and CD-ROM drives in Chapter 7, “Working with Disks.” Right-click on an empty area of the Desktop. When the popup menu appears, select New and then Program. A window will appear, asking you to supply a name for this kdelnk file. Change the name from the default “Program.kdelnk” to a name which represents your program, for example, “Netscape.kdelnk.” An icon which looks like a gear appears on your desktop.

After you have created the icon, right-click on it and choose the Properties command. This will present you with a panel like the one in the following figure.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_104_0.png)

This window controls the properties for the kdelnk file.

Click on the Execute tab to change the settings that associate the icon with the actual program. The Execute panel looks like the one in the next figure.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_104_1.png)

The execute tab allows you to associate a program with the kdelnk file.

If you know the location of the program file, just enter it into the Execute field. For example, the path to the Netscape program is /opt/netscape/communicator/netscape. If you don’t know the exact path, you can also use the Browse button to find the file by hand.

Some programs use a special directory as their working directory where they keep files. When programs do this, they will routinely look in that working directory for the files associated with the program. Such programs would require having the Working directory field filled.

The Swallowing on panel option is for applications like the CD player that become a small icon on the panel when running. The Run in terminal button is for command line programs for which you want to provide an icon.

To associate an icon with the file, click the button containing the gear icon. This will bring up a panel you can use to select an icon for your program (see

the next figure).

![](img/edf072a03d4de1f8f4a13465ac79e7fb_105_0.png)

Use the Select icon panel to associate an icon with your program.

The Select icon panel has a popup menu that you can use to find icons in KDE’s icon area in the /opt/kde/share/icons or in your home directory in the kde/share/icons directory. Note that this directory is typically invisible because it starts with a period; to display it in a KFM window, activate the Show Dot Files option in the View menu. Click on an icon you like, and click OK. (Netscape’s icon is the one that looks like a ship’s wheel.)

> **Check This Out:**
> You can add your own icons using the Paint application. Icons are saved using the XPM format and are 32 pixels wide by 32 pixels high. If you store them in the kde/share/icons directory in your home directory, you’ll be able to associate them.

The final step in configuring the kdelnk file is to associate file types and the name of the program with the kdelnk file. This will allow KFM to associate the icon with the program when you are browsing the file system (see the following figure).

To associate your icon with the actual program, type the name of the program followed by a semicolon (;) in the Binary Pattern field. KDE will use this name to show the icon when you are browsing through the file system.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_105_1.png)

The Application tab associates file types and icons with the program. The comment area is displayed as a ToolTip when you hover your cursor over the icon.

The comment field is displayed as a ToolTip when you hover your mouse over an item displaying this icon.

The application name is the name for the program in your language. If you were editing this .kdelnk file by hand, you would be able to provide multiple translations to the application name.

The two lists at the bottom are special. The list on the left side represents the MIME (Multimedia Internet Mail Extensions) types that the application is able to open. MIME types are sometimes tricky to figure out, but in the case of Netscape, you’ll want to associate the text/html type. To eliminate
