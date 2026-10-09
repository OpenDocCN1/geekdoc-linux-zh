![](bbox=[0.15, 0.09, 0.85, 0.35])

*Figure 4-6. Eclipse Workspace Launcher*

After Eclipse finishes loading, it presents you with a welcome screen.

# Extending Eclipse

As we explained, Eclipse is a modular framework for building IDEs. Thus, apart from the common core framework, most Eclipse-based IDE functionalities are provided by plug-ins. Plug-ins allow Eclipse to support a wide range of languages, source control systems, targets, debugging facilities, and more.

As we chose to install the Eclipse IDE for C/C++ Developers edition, one plug-in is already installed in our new Eclipse installation: CDT, the C/C++ developer support plug-in. In order to make Eclipse a more useful developer environment for embedded Linux, we will add the the Target Management toolkit plug-in and the Subclipse Sub-version source control integration plug-in.

> You can find many more plug-ins (more than a thousand are listed at the time of this writing) in the Eclipse Plugin Central website at http://www.eclipseplugincentral.com.

# Installing a plug-in

Eclipse contains a generic infrastructure for installing and updating plug-ins. Installation of practically all Eclipse plug-ins, therefore, follows the same procedure.