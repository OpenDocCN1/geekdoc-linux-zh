
# Solution Design

The office deployed multi-station systems based on Fedora Core 4 and Desktop Multiplier, each with four or six video heads. Four of the quad-user systems were retrofitted from the existing inventory of workstations by adding video cards and memory, while the two six-user systems required new computers based on AMD's Athlon 64 processor. All systems contained memory to provide between 256 and 512 MB of RAM per attached workstation.

In the new deployment, each multi-user system served four to six users. One of the systems was fitted with four dual-head video cards to accommodate four dual-display systems. A central server running Linux was added to provide authentication services and remotely mounted home directories for each user.

The four users in the executive suite were provided with client workstations connected to another multi-station host. 

Access to optical drives was preserved by positioning multi-station systems (each with a single optical drive) close to the users who anticipated them most frequently. Deploying external USB optical drives (for approximately $30 more than the cost of an additional internal drive) is an option if concurrent and frequent access become necessary in the future.

Minimal changes to the office layout were required to accommodate the new configuration. The most drastic changes were the removal of individual workstations under most employees' desks, and the deployment of storage, backup, and intranet servers based on hardware from the former workstation computers. No additional electrical or network cabling was required to add workstations for the ten new users. An important consideration became installing new cabling and electrical outlets costly.

With the savings from reduced management costs, the office was able to expand the deployment beyond the initial plan to have one workstation for each employee, and the office outfitted every available desk with a workstation. The extra workstations increased flexibility in work patterns and improved collaboration among employees. In addition, an RDP server was set up to provide access to key Windows applications from anywhere in the office using the Open Source rdesktop software at:

http://www.rdesktop.org/

The move to a consistent software platform and patch level reduced demands on the IT staff. The hardware-related savings allowed the office to increase their refresh cycle from four years to two years, ensuring all users have the latest high performance computer hardware. As a result, single image desktops eased management, central storage, and backup-related overhead.

Appendix D. Multi-station computing deep dive using Useful Desktop Multiplier 307 deployment freed up ports on the existing 24-port managed switch for future network growth. The workstation redundancy built into the new setup also allows anyone to work on any other station for collaboration, or to minimize employee down time in case of hardware failure.

# Case study two: Transactional desktops: Public computers for a city library

A multi-branch city library experienced a period of significant growth due to population increases in their area. Library branches were added and modernized to increase services with a focus on electronic access. The highest growth rate was in public computer use. Its eight branches saw a 400% increase in computer hours logged between 1998 and 2003.

# Requirement

Since began deploying public access computers, the library had prized itself on offering its patrons an excellent service. Unfortunately, tight budgets coupled with high hardware, software, and support-related costs were forcing choices on the library. If the branches wanted to meet the immediate demand for computer access for all their patrons, not all of the computers could have the latest software packages. Even free software updates (as the latest version of Macromedia Flash) were often not up-to-date staff was always in limited supply. Many stations lacked floppy drives, because staff time lacked building capabilities, and not all stations could run processes. For years, the library was forced to pick and choose from a limited set of options. They simply could not provide everything patrons wanted on every computer. This created a heterogeneous hardware and software environment that was difficult to maintain and support.

Helping patrons find the correct station to print a resume or download attachments to disk also placed a unwanted burden on the reference desk staff. Supporting the wide array of hardware and software combinations on 100 public access computers across eight branches became a headache for the IT staff. In addition, there were never enough machines to go around and there were often long lineups for computers, particularly during peak hours.

# Solution Design

In 2003, the library's Manager of Systems and Technical Services decided to deploy public access computing solutions for their branches based on User's Desktop Multiplier technology. The library's multi-station solution was built by augmenting standard PCs with multiple dual head video cards with the target of supporting four to eight users per computer.

Replacing a large number of individual workstations with more tamper-resistant multi-station Linux systems drastically lowered support, licensing, and power usage for the library. The multi-station desktop approach also enabled the library to implement a consistent hardware and software platform at all branches, which reduced the burden on IT staff. Further savings were achieved through lowered hardware and software failure rates due to the reduction in the total number of systems they needed to support.

# Additional multi-station case studies

You can read additional case studies and customer references for multi-station Linux deployments at:

```
http://useful.com/customers/case-studies
```

# Understanding how multi-station computing works: Exploiting the flexibility of X Window System

The X Window System (also known as X11 or X) is a windowing system for computer displays, which provides the framework for the graphical user interface found in most Linux distributions. X is responsible for drawing and moving windows on the display and interacting with input devices such as a mouse and keyboard. X does not specify the appearance or behavior of the user interface. Xorg, the current reference implementation of X, is the most commonly bundled and distributed version, although implementations as XFree86 are also popular. For more information, see:

```
http://en.wikipedia.org/wiki/X_Window_System
http://wiki.x.org/wiki/
```

# The design of X

The design of X is based on a client/server model, in which the server communicates with client programs. The X server accepts requests to display graphical output (windows) from the window manager and returns input (keyboard, mouse, and so forth) to the window manager. The window manager running above X (such as Enlightenment or twm) controls the placement and display of application windows. On top of the window manager, GUI widgetkits (such as Qt and GTK) and desktop environments (such as KDE and Gnome) provide the windows with their specific appearance and visual styles.

The X server is capable of keeping track of multiple video cards, monitors, and input devices. Therefore, an X server is capable of logically interfacing with a large array of displays. In a multi-display configuration, X can be configured to present the displays as individual displays or as one large display, or as multiple logical groupings of one or more displays. See Figure D-3.

![](img/23b949da14ff7bab8762f0f0361af394_337_0.png)

Figure D-3 Standard single-user X server

Figure D-3 shows a typical single-station X implementation that uses a single server to handle a single keyboard/mouse input and outputs a single desktop to one or more monitors.

See Figure D-4 on page 311.
