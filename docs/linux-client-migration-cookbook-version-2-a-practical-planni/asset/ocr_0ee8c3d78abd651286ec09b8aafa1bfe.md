> **Important:** If an application is not optimized for terminal servers, it takes the same amount of memory for each instance. The server needs to have enough main memory to handle the expected Terminal Server load.

The connection to the Terminal Server is made by tsclient, GTK+ GUI for the rdesktop application. Using a launcher file on the desktop, it is possible to use a configuration file while executing tsclient. Our command syntax for starting the tsclient session is as follows:

```
tsclient -x $HOME/framemaker.tc
```

The framemaker.tc contains all of the information for the connection, such as the IP address of the host and the username to connect to.

An example window of FrameMaker running inside a Terminal Server client on Linux is provided in Figure 8-1 on page 190.

# Image manipulation

On the Windows-based client, we used Jasc Paint Shop Pro for manipulating images and taking screen captures. Because Paint Shop Pro is not available for Linux, we decided to use the GIMP as a functionally equivalent Linux application instead. This open source application is very mature and provides a good functional equivalent to Paint Shop Pro for the specific uses that the Windows client in this scenario needs. Further information can be found at:

http://www.gimp.org

The GIMP is included as part of the standard installation of Red Hat Desktop, no extra configuration was necessary. A screen capture showing the GIMP running on the migrated desktop is shown on Figure 8-2 on page 191.

# Browser

For our migration scenario, we decided to use the Mozilla Firefox Browser. Firefox is the browser-only project from the Mozilla Foundation. Because we do not need mail capabilities (these are provided by Novell Evolution), using the stand-alone browser offering from Mozilla seemed reasonable.

We recommend that you check important Web sites or especially Web clients for compatibility with the browser before the migration. Some Web sites use ActiveX® controls or special JavaScript™ functions, which are only supported by Microsoft Internet Explorer. Because this is not the case for our migration client, it is easy to make the switch and use Mozilla Firefox instead of Internet Explorer.