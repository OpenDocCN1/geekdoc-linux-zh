Despite Dillo’s limited features, the version we have in DSL is highly modified with several patches that greatly enhance its capabilities. Our version of Dillo can do the following:

+   - Negotiate SSL pages and password authentication
+   - Render frames and Iframes
+   - Text search
+   - Perform GUI configuration
+   - Support referer data
+   - Perform user-agent configuration
+   - Perform gzip compression
+   - Perform meta-refresh

Users of Dillo will be amazed at how fast it loads and how quickly pages render.

For more information on Dillo, refer to the Dillo project site at www.dillo.org. Refer here for details on Dillo internationalization: http://teki.jpn.ph/pc/software/index-e.shtml.

# EmelFM—A Highly Configurable Two-Panel File Manager

EmelFM has a simple-to-use interface; bookmark and history lists; multiaction selection for each file type, filename, size, and date filters; a very handy built-in command line; user-defined menu; loadable plug-ins; and configurable toolbar.

In DSL, we integrate EmelFM into our desktop for the convenience of the user. For example, in the Fluxbox menu, we have both user- and root-level options. We also built in a MyDSL button for extension management and have emelFM use native DSL applications as the default whenever applicable.

Basically, we configure EmelFM so that it works in our lightweight environment; thus, it will call Aterm instead of Xterm, as well as our Wordview Lua program (written by Robert Shingledecker) to view Microsoft doc files. Figure 3-5 shows an example of an EmelFM window.

For details on emelFM, visit its project site at http://emelfm.sourceforge.net/.

# Firefox—The Open Source Web Browser from the Mozilla Foundation

Firefox is a very robust and capable browser. It is by far the largest application in Damn Small Linux, yet we do make provisions to get the size down, including building against GTK1.2 and having our version use system fonts.