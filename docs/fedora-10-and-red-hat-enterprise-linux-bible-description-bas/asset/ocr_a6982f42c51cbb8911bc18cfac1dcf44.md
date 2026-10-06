you need. I recommend the Yum version, which will install the plug-in and make automatic updates of the flash player as they are available.

+   * **MPlayer Plug-in** (http://mplayer-in.sourceforge.net) — This plug-in implements the popular mplayer video player to play embedded video content in the browser window. An RPM package for this plug-in (mplayer-in) is available from http://rpm.livna.org. See Chapter 5 for more using rpm.livna.org.

+   * **Java Runtime Environment** (java-1.7.0-icedtea) — To be able to play Java and JavaScript content from your Web, you need a plug-in that provides the functionality you get with the Java Runtime Environment Web plug-in from Sun Microsystems (http://java.com/en/download/index.jsp). Instead of using proprietary code from Sun, however, Fedora has added a completely equivalent version by combining software from the OpenJDK project and IcedTea project (http://fedaproject.org/wiki/Features/IcedTea).

To sure the plug-in is working, restart Firefox and type about:plugins in the location bar. You can also find a list of Java content handled by the GCJ Web Browser Plugin. You can also try different Web sites that contain Java content to try your Java plugin. For example, you can visit the Java.com test page:

```
http://java.com/en/download/help/testvm.xml
```

If you are unable to see the Java content, the PackageKit Update Applet and for an uspluginwrapper package. Installing that package and restarting your Firefox browser should allow you to see the Java content.

> NOTE: If you are concerned about the experimental nature of IcedTea at the moment, there are other ways of getting a Java Runtime Environment browser-plugin working in Fedora. There are RPMs of that software available from the dag.jweiers.org Fedora repository. Others have had luck getting the software from the dag.jweiers.org. In the past, I have gotten the package directly from sun.com to work, but I found it difficult to get working in the Fedora Release. so you may want to build your own RPM (see www.fedora.org/#faq).

+   **CrossOver Plugin** (http://www.codewavers.com) — Linux plug-ins are not available for some of the most interesting and popular plug-ins. QuickTime 5 movies, Shockwave Director multimedia content, and various Microsoft software, file, and data formats will not play natively in Fedora. Using software built on WINE for Linux on x86-processors, CodeWeavers created the CrossOver Plugin. Although longer offered as a separate product (you may buy the entire Crossover Office product for US$39.95), the CrossOver Plugin lets you play some content that you could not use in Linux. (Download a demo from

```
http://www.codewavers.com/site/products/download_trial.
```