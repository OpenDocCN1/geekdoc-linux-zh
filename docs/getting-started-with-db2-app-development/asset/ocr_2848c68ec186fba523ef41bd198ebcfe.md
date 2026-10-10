# 7.2.1.1 **RubyGems: Locating, installing and upgrading Ruby packages**

RubyGems is the standard packaging and installation framework for Ruby libraries and applications. RubyGems makes it easy to locate, install, upgrade, and uninstall Ruby packages.

A gem, in the RubyGems world, is a packaged Ruby application or library. These files follow a standard format and are stored in a central repository on the Internet. Gems have a name and a version; for example *rake 0.4.16*.

A command line tool also called gem can be used to manipulate these gem files. If you want a gem, you can simply ask RubyGems to install it (and all its dependencies) online. Everything is done for you. *Figure 7.6* shows you how to install the “rake” gem through the internet.

![](bbox=[0.15, 0.36, 0.78, 0.55])

**Figure 7.6 – Installing the *rake* gem**

As shown in the figure, from the machine where you installed Ruby, you can issue the command *gem install rake*. This will connect to *http://rubygems.org/*, and locate the *rake* libraries and the *rake* command-line program. We discuss the *rake* command later; for now, it’s good to know that *rake* is a tool you can use to build other gems. Once the libraries and command-line program are downloaded, they are automatically installed.

# 7.2.2 **Installing Rails**

With RubyGems you can install *Rails* and its dependencies easily just as other gems. Install Rails by following these steps:

+   1. Open a Command Prompt window.
+      Start -> All Programs -> Accessories -> Command Prompt
+   2. Change the directory to <*ruby_home*> and issue the gem command:
+      *gem install rails*
+   
+      It may take several minutes to get all packages installed depending on your network speed. The gem command accesses the *http://rubygems.org/* site to look for the required Rails