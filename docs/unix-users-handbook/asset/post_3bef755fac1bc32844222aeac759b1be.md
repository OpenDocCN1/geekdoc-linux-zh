
foundation for a variety of other useful interoperability between the two operating systems.

## Why the X Window System?

The Windows user environment and the UNIX user environment, which is based on X Windows, are much different. There is no bundled support whatever for accessing Windows from UNIX and UNIX from Windows.

To go beyond logging into a Windows system to perform Windows system administration and logging into an UNIX system to perform UNIX system administration, you need some way of getting access to one of these systems from the other. The X Window System is an ideal way to get remote access to a UNIX system while sitting at your Windows system.

## X Window System Background

X Windows is a *network*-based windowing environment, not a system-based windowing environment. For this reason, it is ideal for giving you a window into your UNIX system from your Windows system.

X Windows is an industry standard for supporting windowed user interfaces across a computer network. Because it is an industry standard, many companies offer X server products for operating systems, such as Windows (we'll get into the "server" and "client" terminology of X Windows shortly). X Windows is not just a windowing system on your computer but a windowing system across the network.

X Windows is independent of the hardware or operating system on which it runs. All it needs is a server and a client. The server and client may be two different systems or the same system; that detail doesn't matter. The server is a program that provides input/output devices such as your display, keyboard, and mouse. The client is the program that takes commands from the server such as an application.

The client and server roles are much different from those we normally associate with these terms. The X Windows server is on your local system (in this chapter, it is your Windows system), and the X Windows client is the application that communicates with the server (in this chapter, it will be the UNIX system running a program such as a System Administration Tool). We normally think of the small desktop system as the client and the larger, more powerful system as the server. With X Windows, however, it is the system that controls X Windows that is the server, and the system that responds to the commands is the client. I often refer to a powerful client as the "host," in order to minimize confusion over this distinction.

In X Windows, the software that manages a single screen, keyboard, and mouse is known as an X server. A client is an application that displays on the X server. The X client sends requests to the X server, such as a request for information. The X server accepts requests from multiple X clients and returns information and errors to the X client.

Sitting on one of the Windows systems on a network, you could open an X Window into several UNIX hosts. You could therefore have one window open to UNIX_System1, another window open to UNIX_System2, and so on.

The X server performs the following functions:

- Displays drawing requests on the screen.
- Replies to information requests.
- Reports an error associated with a request.
- Manages the keyboard, mouse, and display.
- Creates, maps, and removes windows.

The X client performs the following functions:

- Sends requests to the server.
- Receives events and errors from the server.

## X Server Software

There are many fine X Server products on the market. I loaded Exceed 6 from Hummingbird Communications Ltd. on my system for demonstrating how X Windows can be used in a Windows and UNIX environment. I will use Exceed 6 in the examples in this chapter. Figure 15-1 shows the full menu structure from having loaded Hummingbird's X Windows product Exceed.

![](img/75f39fc91296b889c0653851accdfd46_1195_0.png)

Figure 15-1 **_The Programs-Exceed Menu_**

Selecting the Exceed icon from the very top of Figure 15-1 produces a group of Exceed icons that is an alternative to accessing items from the menu of Figure 15-1. Figure 15-2 shows the icon group.

![](img/75f39fc91296b889c0653851accdfd46_1196_0.png)

Figure 15-2 The Exceed Group

The Exceed menu pick from Figure 15-1 allows you to establish an X Windows connection between your Windows system and UNIX system. You can specify the host to which you want to connect, the UNIX system in this case, the user you want to be connected as on the host, and the command to run on the UNIX system. Figure 15-3 shows the Xstart window.

![](img/75f39fc91296b889c0653851accdfd46_1197_0.png)

Figure 15-3 Establishing an X Windows Connection

The window in Figure 15-3 is labeled "DTTERM.XS." After you set up the Xstart window with the information you want, you can save the configuration. In this case, I am issuing the **dterm** command, so I saved the window under this name. The system type can be most any system running X Windows. I used an HP-UX system in the upcoming examples, so the *Host Type* is HP. The complete **dterm** command used will run on most UNIX systems running the Common Desktop Environment and is shown below:

**dterm -background white -display 15.32.165.10:0**

Selecting *Run!* from the window in Figure 15-3 brings up the window in Figure 15-4, in which you can issue the *Password* and make other changes.

![](img/75f39fc91296b889c0653851accdfd46_1198_0.png)

Figure 15-4 Establishing an X Windows Connection

This command starts a **dterm** window, which is a standard window program on UNIX with a white background, and displays the window on the system at the IP address 15.32.165.11. The IP address in this case is the Windows system on which you are issuing the command, which is the X Windows server. The ":0" indicates that the first display on the Windows system will be used for **dterm**, because in the X Windows world, you can have several displays on a system. The system on which the command runs is 15.32.165.10. This is the UNIX system that acts as the X Windows client.

Although you are typing this information on your Windows system, this command is being transferred to the UNIX system you specified in the *Xstart* box. This transfer will have the same result as typing the **dterm** command shown on the UNIX system directly.

When you type your password and click *OK*, a **dterm** window appears on your Windows system that is a window into your UNIX system. Figure 15-5 shows the **dterm** window open on the Windows system.

![](img/75f39fc91296b889c0653851accdfd46_1199_0.png)

**Figure 15-5 dterm Running on UNIX and Displayed on Windows**

Figure 15-5 is a **dterm** window displayed on the Windows system but running on the UNIX system. The window currently has open the HP-UX manual page for **dterm**. You can issue any commands in this **dterm** window that you could issue if you were sitting on the UNIX system directly. Keep in mind, though, that your access to the UNIX system is based on the rights of the user you specified in the *Xstart* window.

You can use *Xstart* to run any program for which you have appropriate permissions on the UNIX system. Figure 15-6 shows an xterm window that is displayed on the Windows system but is running on the UNIX system.

![](img/75f39fc91296b889c0653851accdfd46_1200_0.png)

Figure 15-6 **xterm** Running on UNIX and Displayed on Windows

You are by no means limited to running only terminal windows such as **dterm** and **xterm** under X Windows in this environment. You can invoke your commonly used applications or perform system management functions as well. Figure 15-7 shows the System Administration Manager (SAM), which is the primary system administration tool on HP-UX, running on the UNIX system and displayed on the Windows system with **Kernel Configuration** selected.

![](img/75f39fc91296b889c0653851accdfd46_1201_0.png)

Figure 15-7 SAM Running on HP-UX and Displayed on Windows

You have no reason, however, to limit your use of Exceed to opening single windows or single applications. Exceed can also be used to run the Common Desktop Environment (CDE) used on most UNIX operating systems. CDE is a windowing environment that allows you to open several "desktops," which results in many windows.

By modifying a few parameters in Exceed, you can specify that the entire CDE environment run on your Windows system. CDE allows you to have multiple workspaces in which you can organize the functional tasks you are performing. Figure 15-8 shows CDE running on our Windows system with the first of the workspaces selected called *program*.
