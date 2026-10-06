# Part II: Using Fedora RHEL

whatever:0.1

This address identifies the second screen (.1) on the first display (:0). The first screen is identified as .0 (which is the default because most displays only have one screen). Unless you have multiple physical screens, however, you can skip the screen identifier.

There are two ways to identify your display name to a remote application:

+   **DISPLAY shell variable** — The DISPLAY variable can be set to the system name and numbering your display. After this is done, the output from any X application run from, for example, set the DISPLAY to the first display on whatever, will appear on the display indicated. type one of the following:
```bash
export DISPLAY=whatever:0
or
setenv DISPLAY whatever:0
```

+   The first example shows how you would set the DISPLAY variable on a bash or ksh shell. The second example works for a csh shell.
-display option** — Another way to identify a remote display is to add the -display option to the command line when you run the X application. This overrides the DISPLAY variable. For example, to open an xterm window on a remote system so that it appears on the first display on whatever, type the following:
xterm -display whatever:0

With this information you can access from your local computer. The following sections describe how you may use this information to start a remote X application.

# Launching a remote X application

Suppose you want to run an application from a computer named remotel from your local area network (in your same domain). Your local computer is local, and the remote computer is remotel. The following steps show how to run an X application from remotel from your X display on local.

> CAUTION: This procedure assumes no special security procedures are implemented. It is the default situation and is designed for sharing applications among trusted computers (usually single-user workstations) on a local network. This method is inherently insecure and requires that you trust all users on computers to which you allow access. If you require a more secure method, refer to the section "Using SSH to run remote X applications" later in this chapter.

You may need to enable your X server to support networked connections. If you need to enable networked connections, run the following command: