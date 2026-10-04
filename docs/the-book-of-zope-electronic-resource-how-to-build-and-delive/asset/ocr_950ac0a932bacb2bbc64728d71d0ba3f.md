# 14.2 External Methods

External methods interface with external files (modules) that contain Python methods. These files must have the extension .py and must be located in the Extensions directory of your Zope installation.

External methods allow you to extend the full power of Python into Zope because, when you use them, you are not restricted to specific modules and functions as you are using only Python scripts. However, you cannot edit external methods from within Zope, so you must be able to write files into your Zope installation directory to create external methods.

> NOTE Be careful to code your external methods to avoid creating security holes in your server that can be exploited through the web.

# 14.2.1 Creating External Methods

If you do not have an Extensions directory in your Zope installation directory, create one now: you'll create the external method objects using the Zope management server. These external method objects expose the external Python code so that they can be called from within Zope.

The following explanation assumes that you are in the folder where you want to create the external method object. On the folder's add menu, you will find the entry for creating external methods as shown in Figure 14-5.

![](bbox=[0.218, 0.463, 0.608, 0.793])

Figure 14-5: The add objects menu