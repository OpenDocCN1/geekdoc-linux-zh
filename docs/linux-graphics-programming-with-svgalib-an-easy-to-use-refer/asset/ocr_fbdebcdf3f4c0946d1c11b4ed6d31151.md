X graphics programs (or clients) work by sending their data to the XFree86 server, which then passes the data on to the video card for display. No X client program accesses the video card directly like we do with SVGAlib.

# ## Advantages of SVGAlib

Here's a list of some of the advantages SVGAlib offers:

+   * *Speed*—SVGAlib sends data straight to your VGA card. SVGAlib is like a giant retail superstore that bypasses the middleman to bring you the lowest prices (or, in this case, the best speed). This is especially important in realtime games such as Quake, Doom, and flight simulators.

+   * *Ease of use*—As far as programming goes, the functionality of SVGAlib can't be beat. For the end user, there's no startup time; programs execute instantly. SVGAlib also uses your entire screen and makes it very easy to dictate the display resolution. Many of us prefer this to partial windows and the gimmick of a panning display.

+   * *Comprehensiveness*—You're spared the task of downloading a new server every time you change your hardware. This may not be a major issue, but it's still an annoyance that X saddles you with.

Nevertheless, some people will never be happy with SVGAlib. Here are some reasons why:

+   * *Portability*—SVGAlib functions will only work with SVGAlib and are therefore useless outside of the *Linux environment*. Some people consider this a weakness. They point out that an application written for X Windows doesn't have to be rewritten for another flavor of Unix. This is true, but code written for X on Unix isn't compatible with Microsoft Windows or Macintosh, either, so some amount of rewriting is inevitable. Besides, MS Windows applications work only on one platform, and no one complains about that. This brings to mind Java, the fantastic, solve-all-your-problems, hardware-independent language of the mid 90's. Of course, the reality is a little different. All that these "universal" languages manage to do is make your life more difficult. You're going to have to face the fact that some amount of rewriting is necessary if you migrate to another platform. Besides, given the inavailability of Linux, why would you want to?

+   * *Perceived security hole with* *setuid requirement*—In order to access a hardware device on Linux, you must be logged in as root, or else you must be running a *setuid root process*. Because SVGAlib achieves speed by accessing your video card directly, all SVGAlib programs must be *setuid* root if they're to be run by nonroot users. This alarms some people, but the simple fact is that root privileges are relinquished immediately after initialization, meaning there's no reason to be concerned. As a matter of fact, my system has been hacked a few times, but it was never on account of SVGAlib.

+   * *Inability to display multiple windows simultaneously*—People get really hung up on this one, and I don't know why. This isn't so much a design flaw as it is a matter of the necessary application having yet to be written. And why hasn't it been done? Perhaps because no