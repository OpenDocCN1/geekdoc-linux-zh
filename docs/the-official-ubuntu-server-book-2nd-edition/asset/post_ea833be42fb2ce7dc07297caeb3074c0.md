
When using USB sticks with Ubuntu, you would normally have to unmount the device before removing it physically. This is so that Ubuntu has time to write all the data it needs to the USB stick and can safely unmount it. In the LTSP environment, using a USB stick is a little different. There is no unmount option because the data is written to the USB stick on a very regular basis. Hence you do not need to unmount it and can just remove it once the computer has finished writing information to it.

Local device support is set up by default in Edubuntu; however, to use it you must add to the fuse group the users who require access to such support. You can do this from the user manager. Start by going to System > Administration > Users and Groups option. From here, select the user to whom you wish to give local device access and click on the User Properties button. Click on the User Privileges tab, and from here tick the checkbox for allowing use of fuse filesystems, as shown in Figure 5-16.

![](img/304f637afcecc491b152ee8ac5afadee_252_0.png)

Figure 5-16 Setting fuse preferences

## Sound over LTSP

Since Ubuntu Dapper 6.06, Edubuntu has the ability to play sound through the speakers of the client machine. For versions of Edubuntu prior to 6.10 and LTSP setups installed on top of Ubuntu, you must add an entry to the /opt/ltsp/i386/etc/lts.conf file to enable sound for client machines.

The easiest way to edit this file is to hold down Alt-F2, which will bring up the run command dialog box. Type in the following command:

```
gksudo "gedit /opt/ltsp/i386/etc/lts.conf"
```

Clicking OK will bring up an editing window. Make sure to have at least a [default] section in the lts.conf file where you will add the following line:

```
SOUND=True
```

> NOTE Dapper 6.06 LTS is very particular about the SOUND=True statement. You must type it exactly as shown, taking extreme care with capital letters and so on.

For all versions after 6.10 of Edubuntu, this is already done for you, and sound should work on client machines out of the box.

## CHAPTER 6
Security

SECURITY IS DEFINITELY A HOT TOPIC both inside and outside the computer world. It can be difficult to distinguish legitimate threats from basic paranoia, but as anyone who has connected to a high-speed connection and monitored the logs knows, these days there are armies of servers out there trying to attack you.

Even though other operating systems and products seem to get the majority of the press for their security breaches, Ubuntu users aren’t completely in the clear. Even though Ubuntu has good security out of the box, the moment you set up new services you risk opening holes to attack. This chapter discusses some common security practices and simple steps you can take to keep your Ubuntu server secure. Just in case you still get attacked, I also include a section at the end on how to respond to a security breach.

### General Security Principles

There is a saying in security circles: “Security is a process, not a product.” What that means is that despite what your vendor might tell you, you can’t solve all your security problems with some appliance or software. Instead, you find real security when you follow sound security principles and develop sound security procedures. While I cover some specific tools and options you can use to increase your system’s security later in the chapter, there’s no way I can discuss how to lock down every major service under Ubuntu. These principles, though, are something that you can apply no matter what software you might run:

- Keep it simple.
- Another saying you will hear in security circles is “Complexity is the enemy of security.” The more complex a system, the more difficult it is to understand every part of it and the greater the likelihood that the security of some aspect of the system was overlooked. Whenever you design a system, try to keep the number of interoperating pieces as small as you can. Not only will it help with security, it will help with troubleshooting and overall administration as well.

- Follow the principle of least privilege.
- The principle of least privilege is the idea that programs and people should operate with the lowest possible level of power. This is the
