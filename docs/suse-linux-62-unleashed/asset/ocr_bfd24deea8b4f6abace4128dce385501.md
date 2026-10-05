# System Service Tools
CHAPTER 6

YaST can be used a graphical tool for many different tasks. These include (but are not limited to) 

+   - Configuring and integrating hardware
- Configuring network services
- Hard drive and filesystem management
- Software management
- System installation and updating
- User administration

![](bbox=[0.585, 0.103, 0.943, 0.335])

The yast command is located under the /sbin directory and must be run as root. By configuring your system with the yast command, you'll effect changes in SuSE's main system configuration file, /etc/rc.config. This file is maintained by a separate program named SuSEconfig, also located under the /sbin directory, which is launched as needed after running yast. Whereas yast is a compiled binary program (source is NOT provided by SuSE, Inc.), SuSEconfig is a 1000-line shell script that updates and manipulates your system, using or inserting values in /etc/rc.config.

> Note
You can also manually edit the /etc/rc.config file to enable or disable services, software, or hardware support (such as PC cards), and then run SuSEconfig. However, YaST allows you to do this through its graphical interface, and will properly restart or stop a service for you.

# YaST User Interface

Like most system service tools, YaST features a graphical interface. This interface can be used from the console or a command line of an X11 terminal. The yast command also features a command-line interface with numerous options, as listed in Table 6.1.

Table 6.1 YaST Command-Line Options
| Task or Desired Action | Option |
| Back up a running system | -mask backup |
 Choose install medium (source) | -mask medium |
 Choose to use an X display manager (kdm or xdm) | -mask login |