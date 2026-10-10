As before, we will remove (uninstall) all packages related to nginx before proceeding with the installation from source code (see Fig. 1.11).

![](bbox=[0.09, 0.135, 0.94, 0.34])

Figure 1.11: screenshot

As before, after installing Nginx from source code, we have the latest and up-to-date version of the package (see Fig. 1.12):

![](bbox=[0.09, 0.465, 0.94, 0.595])

Figure 1.12: screenshot

However, when it comes to starting Nginx -and just as what would have happened had we tried to do so in Debian- we will most likely get a **nginx: unrecognized service** error message (see Fig. 1.13).

![](bbox=[0.09, 0.695, 0.94, 0.815])

Figure 1.13: screenshot

This is due to the fact that we have installed the package from sources and therefore the startup script has not yet been put in place. In this case, we can either start the *nginx* daemon by running the main executable from the command line using its full