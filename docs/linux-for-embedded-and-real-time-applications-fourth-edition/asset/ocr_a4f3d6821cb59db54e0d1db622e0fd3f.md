+   * TCF Target Explorer
+   * TM Terminal

6.  Expand *Programming Languages* and select `C/C++ Development Tools SDK`

7.  Click `Next` twice, accept the license terms and click `Finish`.

You are prompted to restart Eclipse for the changes to take effect. Not yet, because now we want to install the Yocto plug-in. Go back to `Install New Software:`

+   1.  Click `Add...` in the `Work with` area
+   2.  Enter `http://downloads.yoctoproject.org/releases/eclipse-plugin/2.3/` in the `Location` field, and provide some meaningful name in the `Name` field. Click `OK`
+   3.  Check both of the entries that show up, click `Next` twice, accept the license, and click `Finish`. Interestingly enough, a `Security Warning` pops up that says the software is unsigned and its authenticity cannot be established. Go ahead and click `OK`.

Now you can restart Eclipse. You will find a new menu option, `Yocto Project Tools`. Also under `Window` > `Preferences` there is a dialog for `Yocto Project SDK`.

The *Yocto Project Software Development Kit (SDK) Developers' Guide 2.3*, available from the Documentation page of the Yocto Project website, has an excellent chapter on using the Eclipse plug-in. It in turn points to a wiki entry, with more details on setting up the plug-in.

# ## Personal Observations

Yocto is probably an improvement over OE-Core. At least it has some graphical tools. Nevertheless, like OE-Core, it is very big, very complex, and requires a steep learning curve. If you can invest the time in really learning it, then it is probably useful.

In the next chapter, we will tackle Busybox, the Swiss army knife of embedded Linux.

# ## Resources

+   [www.buildroot.org](http://www.buildroot.org)—Website for the Buildroot project.
+   
+   [www.openembedded.org](http://www.openembedded.org)—Website for the Open Embedded project.
+   
+   [www.yoctoproject.org](http://www.yoctoproject.org)—Website for the Yocto Project.
+   
+   [http://downloads.yoctoproject.org](http://downloads.yoctoproject.org)—Downloads page for the Yocto Project.
+   
+   [www.python.org](http://www.python.org)—Website for python.
+   
+   [www.embedded.com/design/prototyping-and-development/42184900/Open-Embedded--An-alternative-way-to-build-embedded-Linux-distributions](http://www.embedded.com/design/prototyping-and-development/42184900/Open-Embedded--An-alternative-way-to-build-embedded-Linux-distributions)—An introductory paper on Open Embedded Core. It is a little old, but still useful.
+   
+   [https://hwn.net/Articles/682540/](https://hwn.net/Articles/682540/)—*Deciding Between Buildroot and Yocto* reports on a session at the 2016 Embedded Linux Conference that compared and contrasted Buildroot and the Yocto Project.