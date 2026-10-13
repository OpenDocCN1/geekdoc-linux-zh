# WHAT IS AN X APPLICATION SERVER?

The X Windows System, the graphical environment for UNIX and Linux, offers the capability to display applications on remote hosts on the network. This means an application running on one host can be displayed and used interactively on another. The capability to distribute X applications, effectively separating the user interface from the processing, makes it possible to deploy X application servers.

An X Windows System application server is a system that accepts logins from X desktops (which can be special hardware X terminals) and then runs applications that are displayed on these desktops. Using this mechanism, you can deploy X applications on centrally managed servers and thus focus the hardware power for processing and running these applications in a few servers. This limits the need for powerful, complex hardware on the desktop.

This type of centrally managed application environment offers the promise of reduced total cost of ownership because desktops become essentially dumb graphical terminals which do not need individual configuration and can easily be replaced when they fail.

# UNDERSTANDING THE RELATIONSHIP BETWEEN CLIENT AND SERVER IN THE X WINDOWS SYSTEM

When X applications are run remotely in the fashion just described, a strange thing happens: The terms client and server become confused and unclear. A distinction is made between the X application program and the X Windows System.

In the context of requesting and running an application, the user sits at a workstation that is the client from which a request is made to run an X application on a remote X application server. The application executes on the remote X application server but its input is received from, and its output displayed on, the client workstation. This is quite straightforward because the client and server terms apply as they are normally understood.

However, in the context of the X Windows System environment itself, the terms are reversed. X consists of two components: the X server and the X client. The X server program runs on the client workstation, and renders the graphic display of the application. The X application program is the client, issuing rendering commands to the X server program running on the client workstation. The X client program can be running on the local workstation, or on a remote X application server. Notice how the client and server roles are reversed in the X Windows System context.

In the distributed X environment of an X Windows System application server, the X server runs on the client desktops and the applications, which are clients to these X servers, run on the X application server.

Therefore, the client terminal runs an X server and the X application server runs X applications, which are clients of the X server. The fact that the applications running on the X application servers are X clients actually is logical: The applications request the service of the