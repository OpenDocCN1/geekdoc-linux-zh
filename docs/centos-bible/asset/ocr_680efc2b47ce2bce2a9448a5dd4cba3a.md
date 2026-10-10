report where it finds modems. If it tells you that no modem was detected, it's likely that either your modem isn't connected properly or no driver is available to support the modem. 

If the modem wasn't detected, you should determine whether or not it is a modem supported in Linux. You can do this by finding out what type of chipset is used in the modem. This is even more important than finding out the manufacturer of the modem because the same manufacturer can use chips from different companies. This applies primarily to internal, software-based modems because most external serial modems, internal PCI controller-based modems, and many USB modems are supported in Linux. 

After you have determined the chipset being used, check the web site \texttt{11modems.org}. This site contains information on so-called Win-modems. Search for the chipset on your modem from this site. It will tell you if there is a driver available for your modem. 

A nice tool for determining what type of Win-modem you have and how to get it working is \texttt{scanModem}. If you have access to the Internet from another machine, you can download \texttt{scanModem.gz} from \url{http://11modems.technion.ac.il/packages/scanModem.gz}. 

Because you probably don't have a working Internet connection yet, find a way to copy \texttt{scanModem.gz} to your Linux system. As \textit{root} user from a Terminal window, type these commands, with that file in the current directory:

```
# gunzip scanModem.gz
# chmod 755 scanModem
# ./scanModem
```

The result is a \texttt{Modem} directory containing text files describing your modem and what you can do to configure it.

> NOTE 
> 
> If you are a new Linux user with a Win-modem and you are still baffled after referring to \texttt{11modems.org}, you might consider getting a serial or USB modem. To try to get your Win-modem working, you might need to download, compile, and load a \textit{modem driver}. Especially with some older Win-modems, drivers have not been updated to work with the latest kernels. Picking up a cheap serial modem from a used computer store can save hours of frustration that may still result in failure.

# Checking That Your PPP Interface Is Working

One way to check that the PPP interface is working is with the \texttt{ping} command. From the Terminal window, type \texttt{ping} along with any Internet address you know. For example:

```
$ ping www.handsonhistory.com
PONG handsonhistory.com (198.60.22.8) from 192.168.0.43 : 56(84) bytes of data.
64 bytes from handsonhistory.com (198.60.22.8): icmp\_seq=0 ttl=240 time=120 msec
64 bytes from handsonhistory.com (198.60.22.8): icmp\_seq=1 ttl=240 time=116 msec
64 bytes from handsonhistory.com (198.60.22.8): icmp\_seq=2 ttl=240 time=120 msec
```