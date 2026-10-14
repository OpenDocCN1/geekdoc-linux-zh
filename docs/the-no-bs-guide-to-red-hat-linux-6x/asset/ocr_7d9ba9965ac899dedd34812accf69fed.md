Many users actually prefer to use text-based clients (tools that enable end users to connect to various types of Internet servers) because the graphical environment adds a lot of overhead, slowing things down. And some people just prefer the keyboard to a mouse.

> NOTE: It’s important to know the basics of using the Net from a command line, since you might not want (or have the hardware) to run X Windows on your system. These same techniques will come in handy if you have a Unix shell account through your ISP.

# USING FTP

FTP (which stands for file transfer program or file transfer protocol, depending on how many pencils you wear in your pocket protector) is the Internet file mover. You use it to transfer files from one computer to another. Most often, you’ll be using it to download software to your computer, so try that now. To start a text-based FTP client from your Linux command line, enter the ftp command followed by a site name, like this:

```
ftp ftp.devolution.com
```

When prompted, specify anonymous as the log-in name and your email address as the password. You’ll be connected to devolution.com’s FTP site, where you can download Maelstrom—a cool Asteroids-like game for X Windows. After getting logged in to the server, you can enter these commands to download the compressed binary file for Maelstrom:

```
bin
cd /pub/maelstrom/Maelstrom-binaries/linux-x86/
get Maelstrom.tar.gz
quit
```

Use the help command if you’re not familiar with FTP. After the get command is finished, quit will return you to the Linux command prompt, and you’ll have a file named Maelstrom.tar.gz in the current directory. To uncompress the file and create the executable on your system, enter this:

```
tar xvfz Maelstrom.tar.gz
```