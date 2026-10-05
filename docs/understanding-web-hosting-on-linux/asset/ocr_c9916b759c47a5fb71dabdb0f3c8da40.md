# Linux Operation, Configuration, and Administration • 149

# # Facility Configuration and Administration

There are many different aspects to configuring and administering a Linux box that quite a number of books have been written on the subject. This section boils Linux configuration down to one simple fact: almost without fail, you can find the configurations for the operating system and programs in the main /etc directory, or one of the other "etc" directories, such as /opt/etc or /usr/local/etc.

Our initial plan for this section was to show some examples from within /etc directory, point out how to edit them, and then go on talk about the various KDE, Gnome, or Linux utilities that you could use to accomplish the same task. The problem is, like so many things Linux, there are many ways to accomplish this, and there are some risks to advocating a particular method. For example, the linuxconf utility is mentioned in many books as the primary way of configuring your system. However, it is officially deprecated by Red Hat, a polite way of saying it's broken, it's not supported, and it's unlikely to ever be fixed. As a matter of fact, it is so broken that, if you see references to it anywhere on your system, you should go out of your way to avoid it. As we can both attest, its use is likely to destroy your working configuration.

There have been other attempts to configuring your system less of an arcane art and more of science, but they all have been made obsolete by what has to the best configuration tool ever: Webmin. It not only allows you to easily configure your system, it slices and dices to maintain it as well! Webmin is all you need to configure and maintain your Linux server. (If you are a system administrator, however, you will still want to purchase some Linux administration books to explore the guts of the system.)

Webmin is a browser-based application that allows you to configure and manage your computer locally (from the same machine), or from another across a network. So complete is the implementation that you can replace all other configuration tools with this one. As a bonus, it is extensible, so that any software author can write a Webmin module to support his or her application. Webmin, will upon installation, determine the distribution of Linux (and some other operating systems) on which it is running and automatically configure itself to provide only the relevant options. But we digress. You first need to get and install Webmin.

Point your browser to http://www.webmin.com/webmin/ to get the Webmin RPM. To ensure you don't have conflicts with the browser distinguishing between a RealPlayer file and an RPM file, hold the Shift key while clicking the link to save the downloaded file a place to reside, which is probably your home directory, and a name, which is probably webmin-0.90-1.noarch.rpm (although the .90-1 could be different as the program is updated).

Once the file is downloaded, open a terminal window to get a command line, and then issue the su command to switch to the root user (You aren't logged on as the root user already, are you? You shouldn't be!) At the prompt, enter the following command to install the package:

```
rpm -Uvh webmin-0.90-1.noarch.rpm
```

> Tip: Everything through webmin in the line above, and press Tab. The file name will be completed for you through the magic of the bash shell.

After waiting and gnashing of disk, you'll be rewarded with a prompt that says you can log on to http://localhost:10000. That means the Webmin server is ready to accept connections, but is awaiting the connection on port 10000 instead of the standard HTTP port 80. You may now exit the terminal session