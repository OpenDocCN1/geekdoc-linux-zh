Within this open and flexible model, a new generation of solution stacks can combine the best characteristics of proprietary applications and free open-source software to challenge the marketplace, spur development, further design innovation, and extend market opportunities into new, previously untapped areas.

# Difficulties in targeting the Linux Desktop Operating System

Ian Murdock, Chief Technology Officer of the Free Standards Group, has been involved in standards development since the evolution of UNIX in the early 1990s through the current effort to evangelize the benefits of LSB and bring coherence to Linux OS development. "Previously—Murdock said, "developers would have to sit down and create the distribution target—maybe Red Hat, Novell, and Debian—then create individual ports for each of those distributions."

Particularly on the desktop," Murdock continued, "there is no standard way to do some pretty things—like create an icon on the desktop or interface with the printing subsystem. Just to do some of those basic things, you have to make assumptions about the environment that you are running. And that includes not only which distribution you are running, in the desktop case, but also which desktop environment you are running. For example, there might be different ways to add an item to a menu, depending on whether the user is running GNOME or KDE. This is true even on the same version of the same distribution. The key issue is: as a software developer writing an application for a platform, you want to pick the platform that gives you the greatest reach into your market.

> LSB essentially provides a single platform that an application developer can target. Applications typically work across all distributions compliant with LSB. It is all about maximizing the addressable market.

Ian Murdock, Chief Technology Officer, Free Standards Group

In the current worldwide marketplace, distributions are often along geographical limits. What is popular on the desktop in the United States might be completely different from what is popular on the desktop in Asia. If the developer is targeting a specific geography, this makes it easier to choose the appropriate distribution. But it also immediately places limitations on the overall addressable market.

Prior to 3.1, LSB has been focused primarily on core components such as C and C++ run-time environments, areas typically associated with server applications. With the LSB core firmly established as an ISO standard, the LSB 3.1 release targets a higher level up the stack. LSB 3.1 starts at the lowest levels of desktop technologies, such as the popular graphical user interface toolkits GTK and Qt*