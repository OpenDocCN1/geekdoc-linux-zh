This will create a file called *Configuration* in the *src/* subdirectory. It also generates the makefile that will be used to compile the server code.

Once this step is done, type *make* to compile the server code. After the compilation is completed type *make install* to install the server. You can now configure the server via the configuration files. See the section “Runtime Server Configuration Settings” for more information.

# Note

> The Apache Autoconf-style interface (APACI), described here, is only available in version 1.3 and later.

# The Advanced Way

If you want to do things the old-fashioned way, or you just want more control over the way that your server is built, follow these steps:

+   1. In the source directory, copy the file *Configuration.templ* to *Configuration* and open up *Configuration* with your favorite editor.
+   2. Modify the compiler flags if, and only if, you know what you're doing.
+   Uncomment those modules that you would like included, comment out modules that you don't want, or add lines for custom modules that you have written or acquired elsewhere.
+   3. Run the *Configure* script to create the *Makefile*.
+   4. Finally, compile and install the server with *make* and *make install*.

# Tip

> You may want to symlink, using the *ln* command, the existing file locations (listed in the RPM installation section earlier in this chapter) to the new locations of the files because the default install locations are not the same as when the RPM installs the files. Failure to do this could result in your Web server process not being started automatically at system startup.
> I would strongly recommend that you stick with the RPM version of Apache until you really know your way around what happens at system startup.