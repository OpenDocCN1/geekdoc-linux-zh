```
verify script:

(none)

#
```

In this particular case, the xfce86 package has two scripts: One labeled postinstall and one labeled postuninstall. As you might imagine, the postinstall script is executed just after the package's files have been installed; the postuninstall script is executed just after the package's files have been erased.

Based on the labels in this example, you'd probably imagine that a package can have as many as five different scripts. You'd be right:

+   The preinstall script, which is executed just before the package's files are installed.
+   The postinstall script, which is executed just after the package's files are installed.
+   The preuninstall script, which is executed just before the package's files are removed.
+   The postuninstall script, which is executed just after the package's files are removed.
+   And finally, the verify script. While it's easy to figure out the other scripts' functions based on their name, what does a script called verify do? Well, we haven't gotten to it yet, but packages can also be verified for proper installation. This script is used during verification. (For more information on package verification, see section 6.1 in Chapter 6, "Using RPM to Verify Installed Packages.")

Is this something you'll need very often? As in the case of displaying file states, not really. But when you need it, you really need it!

# 5.2.2.11. --queryformat: Construct a Custom Query Response

Okay, say you're still not satisfied. You'd like some additional information, or you think a different format would be easier on the eyes. Maybe you want to take some information on the packages you've installed and run it through a script for some specialized processing. You can do it, using the --queryformat option. In fact, if you look back at the output of the -l option, you'll notice that RPM was using --queryformat internally. Here's how it works: On the RPM command line, include --queryformat. Right after that, enter a format string, enclosed in single quotes (').

The format string can consist of a number of different components:

+   Literal text, including escape sequences
+   Tags, with optional field width, formatting, and iteration information
+   Array iterators

Let's look at each of these components.