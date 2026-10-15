
![](img/5d4d3092919d1d16884788127447cc6d_468_0.png)

## FIGURE 19.1

xeyes, xterm, and xclock are Linux programs running via X-Win32, whereas the My Computer window is native to Windows 98.

- Rootless with custom window manager—The X server can place X programs on the host OS's screen, using a UNIX-style window manager (something that resembles mwm or fvwm is common). This makes the Linux programs look distinctive, but they still integrate seamlessly with the native OS's programs. Figure 19.2 demonstrates eXodus using this approach.
- Rooted—The X server can create its own window and then place X programs in that window exclusively. The separate window can then include desktop backgrounds, X icons, and so on. To get a usable amount of space, though, you might need to size the X server's window so large that it obscures native programs you're using. One variant on this theme is to have the X server take over the entire display, eliminating native programs (a special keystroke will often switch between X and native-OS displays). XFree86 running under OS/2 takes this approach. Figure 19.3 demonstrates MI/X running rooted.

![](img/5d4d3092919d1d16884788127447cc6d_469_0.png)

## FIGURE 19.2

When using a custom window manager, the X programs (xeyes, xterms, and xclock) look quite distinctive, compared to the native Macintosh windows (the Finder window called Orange).

![](img/5d4d3092919d1d16884788127447cc6d_469_1.png)

## FIGURE 19.3

The MIX window contains within it the Linux programs running in MIX's window manager, while Windows programs are entirely separate.

Because most of the commercial X servers have demo versions of some sort, you can try several of them to see which program best suits your needs. X-Win32 is used in the examples throughout the rest of this chapter.

## X Terminals

If your only reason for having PCs is to use them as X servers for a Linux computer, you might want to consider purchasing X terminals instead. An X terminal is a computer that typically contains no hard disk and very limited RAM and CPU power. It functions exclusively as an X server, so you can think of it as a dumb terminal for X. X terminals often come with large monitors, which means they're often expensive. They are quiet, though, and aside from the monitor size, they are compact. If you have an outdated PC, you can effectively turn it into an X terminal by installing Linux on it and configuring it to function as an X server for another machine. This can be a great way to extend the life of an old PC.

Configuring an X terminal is well beyond the scope of this book. If you want to use one with Linux, I suggest you read the NCD X Terminal Mini-HOWTO, which comes with most Linux distributions. Some of the information in the rest of this chapter applies to X terminals, too, so you can glean some information from this chapter. X terminals generally use the X Display Manager (XDM) logon method described later in the next section.

## Logging On

There are two main ways to use an X server: by a textual login start or by an X Display Manager (XDM) login. Each method has advantages and disadvantages.

## Textual Login

A textual login is generally the easiest way to begin using an X server. The idea is that you log in to your Linux computer by using telnet or a similar program and launch your X-based programs from that telnet session. Here's an outline of what to do to use this method:

- 1. Log in to the Linux computer by using telnet, ssh, or some other text-mode remote-access program.
- 2. Set the DISPLAY environment variable to point to the computer on which you want to run the X server. If you're using the bash shell, you can do this with a command such as export DISPLAY=local.machine.name:0.0

You issue this command on the remote machine (that is, through your telnet login). local.machine.name is the name or IP address of the machine at which you're sitting. The 0.0 part of the DISPLAY variable tells the Linux computer which display to use on the server. If you're using a Macintosh or Windows computer, 0.0 or 0 is almost always correct. If you're using another Linux computer on which you have several virtual X sessions running, you might need to use a higher value, such as 0.1 or 1.
