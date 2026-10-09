Speed The CLI is definitely the fastest interface. Using the command line, you can execute a program or edit a configuration file before you can even find the files within the GUI environment. For that matter, you can usually connect to a server, change a configuration file, and restart the affected services before a GUI even starts.

GUI operating systems are not known for their speed. A CLI often can start in seconds, whereas a GUI may take minutes to start. When editing a configuration file, you may have to use a mouse to browse for the file, switch to the keyboard to make changes, switch back to the mouse to save the file, and then use the mouse to find and restart the affected service.

Overhead A CLI requires little in the way of overhead. With today's machines, the resources available usually greatly exceed the requirements of the user interface. On a server, however, the resources are used for applications other than the user interface. For example, a server may provide database access, file space, network services, or application services that require a large amount of resources. A command-line interface allows configuration and management of the operating system without using many resources.

A GUI requires a lot of computer system resources. Specifically, a typical GUI requires many times the amount of RAM and disk space used by the CLI. In most cases, the GUI is the least required application on a server system, but the most required on a non-server system.

Availability On a local machine, both interface types can be made available easily. Remote machines can also provide access to either interface type; however, remotely accessing the GUI is much more difficult.

Linux is designed to be accessed remotely. For example, the telnet application is standard on most systems. Because the CLI requires so few resources, information can be easily transferred to and from computers on a network. Remote administration can be accomplished easily from any machine on the network through such programs.

GUI availability with remote computer systems requires that a server application be running on the remote system and a client application be running on the local machine. The amount of bandwidth required to transfer GUI information to and from computers on a network is large, making its use over dial-up connections nearly impossible, and even with a very fast, high-bandwidth connection the display can be very slow.

Learning Curve The command line requires a lot of training. Just knowing where the configuration files are located and what they control can be a daunting task. As a result, it can take months to become proficient in the use of the CLI.

The GUI interface has a much lower learning curve. The interface is intuitive, and configuring even the most complicated server applications is easy with the provided prompts and integrated help files. Learning the GUI is much faster than learning the CLI.

Usefulness The usefulness of an interface depends on what it is used for and the experience of the user. If you are using the GUI on a server and you are proficient in the CLI, the GUI is just excess overhead and not useful. However, if you are using the Linux system for word processing and other personal productivity applications, the GUI is needed.

A new administrator may use the GUI to help learn how to control the Linux system. For example, an administrator may use the GUI tool to configure Samba and then examine the configuration files to see what was changed by the GUI to configure the system.

An experienced user may use the GUI for most of their work with personal productivity applications; to delete a file, however, the user may find it much faster to open a terminal session and use the rm command instead of starting a GUI file manager and then browsing for the file.

Both interfaces are useful. Different users sometimes need to use different interfaces. Even an experienced Linux server administrator may find that the GUI is required for some services. For example, the Oracle database requires a GUI tool for some of its configuration. Most users will benefit from learning both interfaces.