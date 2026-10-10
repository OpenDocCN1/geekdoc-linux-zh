![](bbox=[0.04, 0.1, 0.17, 0.18])

# Trashing your dial-up options

When you tried to connect, did you get an error that pppd died unexpectedly (what a phrase!) or timed out? If so, contact your ISP to ask what options need to be set in the /etc/ppp/options file. In many cases, an empty options file — or no file at all — does the trick. As root, rename the /etc/ppp/options file to options.old in case you need to return to the original. Then create a new /etc/ppp/options and leave it empty or don't create a file at all!

![](bbox=[0.14, 0.38, 0.6, 0.55])

Please, tell me you made it! If so, you're ready for a cyberspace cruise in Chapter 15.

# Connecting and disconnecting

After you have the dial-up working, connecting to your ISP is a no-brainer. Choose *Application* Starter \Applications \Applications Network \Dial-Up\ and then click Connect. Unless you changed the default setting, Dial-Up remembers your login ID and password from the previous session.

The Connect button becomes Disconnect after you're in. Simply click Disconnect when you want to end the session. The session also terminates if you log out of the desktop.

# Hooking into a Local Network

Dialing up from home to your ISP is one form of networking. Usually when we speak of a *network* though, we're talking about a *local area network* (LAN).