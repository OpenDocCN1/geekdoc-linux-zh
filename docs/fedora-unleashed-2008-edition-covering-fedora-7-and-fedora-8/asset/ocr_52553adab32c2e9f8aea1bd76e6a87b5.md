![](bbox=[0.06, 0.1, 0.64, 0.4])

FIGURE 9.1 Be very careful: Frozen Bubble can become extremely addictive!

A historical gripe of Linux users has been the difficulty involved in getting modern 3D graphics cards working under Linux. Thankfully, since ATI (one of the major graphics card vendors) was bought up by AMD, they have released a true open source driver that is available to install under Fedora. NVIDIA also supports Linux, albeit by using closed source drivers. This means that Fedora does not ship with native 3D drivers for NVIDIA cards. It is fairly easy to get hold of the driver and install it; the Livna.org site has RPMs that are ready and waiting to be installed using yum.

# Installing Proprietary Video Drivers

Fedora does not provide the official NVIDIA or ATI display drivers because they are closed source and Fedora is committed to delivering a totally free (as in speech) distribution. You can download the latest official drivers from http://www.nvidia.com/object/linux.html or from http://www.ati.com/. If you encounter problems with the NVIDIA drivers in particular, check out http://www.nvnews.net/vbulletin/forumsdisplay.php?f=14 for more help. The NVIDIA staff do contribute to that forum, so you should be able to find expert help when you need it.

Bear in mind that if you go down the “official” route, you will have to take certain steps. It would be great to be able to access the drivers through yum, so much so that the Livna repository now has prepackaged the drivers into an RPM that is easily downloaded as long as you have the Livna repository enabled for yum.