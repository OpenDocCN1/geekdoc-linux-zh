On the whole, X’s network–centric nature makes for a great deal of flexibility in a network environment. You can run the same programs *from* many computers, while running these programs *on* just one computer. The complexity and speed hit of X can be a drawback on an isolated workstation, however.

# ## X Security

If you’re using X only locally, chances are your distribution has configured X in a reasonable way. On some distributions, however, you may need to loosen security a bit if you want to use X programs after you’ve used su to acquire root privileges. If you want to run X programs remotely, too, you’ll need to make a couple of adjustments.

# ### Setting X Client Security Options

To use an X server, the client computer has to know *which* X server to use. This is done through the DISPLAY environment variable, which you can set using the following command (assuming you’re using the bash shell):

```
```
$ export DISPLAY=hostname:displaynum
```
```

In this command, *hostname* is the name of the computer on which the server runs (that is, the computer at which you’re sitting), and *displaynum* is the number of the display. *displaynum* is normally 0 or 0.0 for the primary X display, but it may be a higher number if the computer runs multiple X servers, as described shortly in “X Virtual Consoles.” It’s important to realize that you issue this command on the computer that hosts the X programs you intend to run, not on your local computer.

# ### Using *xhost* on the X Server

Most X servers are configured by default to refuse connections except from the local system. Some distributions also refuse connections except from the user who’s logged on locally. When this happens, you won’t be able to use X programs after you use su to acquire root privileges. There are various ways to tell X to be more lenient in the connections it accepts. The simplest is to use the xhost command, which uses the following syntax:

```
```
xhost  [+|-] hostname
```
```

To add a client to the list of allowed hosts, use *+hostname*; to remove a client, use *−hostname*. If you omit the hostname, the X server accepts *or* refuses *all* connections, no matter what the client. This can be a potentially major security problem when adding permissions. Unlike the DISPLAY environment variable, this command must be issued on the X server computer—the one at which you sit.

> **Tip** If you regularly run programs on a variety of computers from a single Linux computer, you can add appropriate xhost commands to your .xsession or other startup file (described later in this chapter) to allow these connections by default. You can use localhost as the *hostname* to ensure that all local users (including root) can use your display, so you can use su and then run X programs as the alternative user.

As an example, consider the following: You’re sitting at the computer dino.pangaea.edu, and you want to run a program that’s located at latch.threeroomco.com. Assuming both computers are Linux or Unix boxes, you would follow these steps:

325