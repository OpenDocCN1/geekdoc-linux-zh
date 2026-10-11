If you are looking to run X from bootup, you can run Linux at run level 4. This will start xdm, the X display manager, which saves users having to run startx every time they log in. However, if your X server starts giving you fits, you might have some problems trying to fix them. In addition, you'll have to change your run level or reboot into single-user mode.

![](bbox=[0.09, 0.215, 0.185, 0.295])

Chapter 6 provides more information on run levels.

# Security and X

A major advantage of X is its network transparency — which can also create a security problem. X is transferred over a cleartext session, which means anyone with a sniffer can access the data. Using X also means you'll have another port open on your network, which in turn means that your host is more vulnerable to attack from the network.

Provided you can control the potential security issue raised by X, it's also possible to let other computers run X applications on your terminal. To control which computers can do so, use the `xhost` command:

```
# xhost +
```

# Fun with X

I taught a UNIX fundamentals class last year and showed the students the joys of X (so to speak). One such delight was `xeyes` — a cute-but-useful application for finding your cursor — as well as how to use `xhost`, and how to send `xeyes` to a neighbor's X display. The command looked like this:

```
$ xeyes -display neighbor:0.0
```

Some of the students had figured out that the up arrow in some shells enables you to go back and reuse a command — and promptly sent 20 xeyes displays to their neighbors' X displays. This made for an amusing class — as long as it stayed in class.

If you can do this operation with a harmless application, consider the possible damage if an intruder tries the same hijinks with a hostile X application. The lesson for administrators is straightforward: Don't allow just anyone to use anyone else's X display.