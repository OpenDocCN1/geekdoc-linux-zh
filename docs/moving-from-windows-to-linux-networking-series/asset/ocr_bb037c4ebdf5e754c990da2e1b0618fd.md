# **FTP Clients**

FTP (File Transfer Protocol) is how you get files across the Internet. If you have ever downloaded something from a Web page, you were using FTP from within the Web browser. You can also use FTP client applications that are for connecting to a specific Web site and uploading or downloading files. If you decide to put up your own Web site, it is likely that the Internet service provider or Web hosting company will give you an FTP address. You would then use your FTP client application to upload new Web pages, change names, alter files, and so on. With Linux you have several options for FTP clients, and we will look at one such option, gFTP, shown in **Figure 13.31**.

![](bbox=[0.06, 0.23, 0.655, 0.58])

**Figure 13.31**: The gFTP application.

On the left side you see a list of all the directories and files on your computer. Once you connect, the right side will show those directories and files on the FTP host computer that you have access to. You can then drag and drop files from one side to another. How do you get connected in the first place? Notice at the top of the screen the boxes labeled Host, Port, User, and Pass. In the Host box you will enter the address of the FTP host computer. This could be a URL, much like a standard Web address, or it could be an IP address like 10.10.10.x. You then type in the port.

**Note** Throughout this book you will see IP addresses much like this one. Real IP addresses on the Web are not generally 10.10.10.x. However, there are a lot of IP addresses in use, and it was necessary to make certain that a real IP address for a real server on the Web was not used.

The host and port information will have to be given to you by whoever is giving you access to the FTP server. However, if no port information is given, the default port for FTP is 21. The Username and Password fields are rather self explanatory. Once you have filled these in, click on the Computer icon to the left of Host, and it will attempt to connect.

For those readers who have an interest in developing Web pages, the FTP client will be very important. Without it, you may have trouble accessing your Web server to upload your Web pages. Many Web hosting services give you a login name and password and ask you to use FTP to upload files to their Web server. Also, in a later chapter, we will be exploring the use of FTP servers in Linux.