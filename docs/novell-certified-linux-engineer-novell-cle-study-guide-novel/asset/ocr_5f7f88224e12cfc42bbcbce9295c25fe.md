The best way to configure this file depends on your organization's standards. Some will direct that iPrint printers be created only for the individual Windows users. Others may not be quite so rigid. When you're done configuring this file, you're ready to complete the last iPrint configuration task: creating printer location maps.

# ## Creating Location-Based Printer Maps

iPrint can be configured to display the Printer Agents associated with the iPrint server in two different ways. The first way is called the list view. As shown in Figure 9.22, when you access the iPrint web page, located at `http://your_server_IP_address/ipp`, with Internet Explorer, a simple list of configured printers is displayed. This is the default view for your iPrint server.

![](bbox=[0.036, 0.361, 0.911, 0.462])

This display is nice, but it seems rather dull to me. You've probably noticed that throughout this chapter I've referred to the fact that you can configure iPrint to display an office map with printer icons that users can use to access printers.

This is the second way Printer Agents for your iPrint system can be displayed. In my opinion, this is the best way to do it. It provides users with an easy way to pick the printer they want to print to. iPrint comes with the iPrint Map Designer, which is a simple web-based tool that you can use to create a customized map for your organization.

To do this, you will need a Windows workstation that has Internet Explorer 5.5 and the iPrint Client installed. You'll also need a graphic (in BMP, GIF, or JPEG format) of your office's floor plan. If you just want to experiment, NNLS includes a couple sample maps in the `/var/opt/novell/httpd/htdocs/ippdocs/images/maps` directory. We'll use these sample maps later in a lab exercise for this chapter.

Once you have your workstation and your map image files ready, you can configure your location-based printing maps by doing the following:

+   1.  On your Windows workstation, map a drive to a Samba share on your NNLS server.