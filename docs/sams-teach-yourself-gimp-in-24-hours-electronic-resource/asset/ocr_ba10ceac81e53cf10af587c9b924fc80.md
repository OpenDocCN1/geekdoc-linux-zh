# Basic GIMP Tools

Start xfstst as a background process:

xfstst &

Tell the running X11 server about the new font server:

xset +fp unix::/7100

Add the new font path to the X11 config file (probably /etc/X11/xF86Config):

FontPath "unix:/7100":

You should now be able to bring up the GIMP Text dialog box and see your TrueType fonts. After installing xfstst, you might want to get it to start automatically every time Linux boots (not that Linux ever rebooting) by adding a reference to it in /etc/rc.local. This keeps you from having to start the TrueType Font Server every you start X. One caveat: if you do this, make sure that you add the full pathname to rc.local, as in /usr/X11R6/bin/xfst_, especially if you use xdm to start a graphical login automatically at startup.

Also, you might not want to load every TrueType font you own, but instead be selective with the TrueType fonts you want to use in Linux. Linux is a handy application but it can suck up a little RAM if left to load 200+ fonts. If you've found it best to use only 30 or so of the best fonts installed. And, there are other TrueType servers out there as well, although I have not personally used them yet. One server is called xfstst, which uses the Free Type library and has had a lot of positive review. It's available online everywhere xfstst is, so you might want to check it out. You can grab a RPMs of Xfree86 with integrated TrueType font support via xfstst from http://www.darmstadt.gmd/~pommnitz/xfstst.html.

# Summary

The essential concepts in dealing with a graphics application such as the GIMP have been covered during the first three hours. Before any real techniques can be applied, you must have an understanding of the basic tools illustrated here. In the next few hours, you will move on to mastering these concepts in order to create some interesting images and effects. You might be surprised at what can be accomplished using only these simple tools. And, gaining mastery over them will give you edge when confronted with specific graphics issues, as image restoration or simple manipulation.

![](bbox=[0.883, 0.353, 0.955, 0.433])