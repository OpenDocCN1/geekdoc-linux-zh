# # Administering eDirectory on Linux

**Test Objectives Covered:**

+   5. Perform eDirectory administration tasks.

There are three main tools you will use to administer eDirectory on Linux:

+   - Command-line utilities
+   - iManager
+   - iMonitor

In this section, we will discuss the basics of each. We will also relate how to perform an eDirectory health check.

# ## Command-line Utilities

On the Linux platform, eDirectory includes several utilities that can be used from the command line to manage your eDirectory database. A detailed discussion of each utility is beyond the scope of this book. We will use iManager and iMonitor as the primary administration tools, wherever possible.

The command-line eDirectory utilities included in NNLS are listed in Table 5.3.

**TABLE 5.3**
# eDirectory Command-Line Utilities

| UTILITY | DESCRIPTION |
| :--- | :--- |
| /etc/init.d/ndsd | The ndsd init script is used to start and stop the eDirectory service on your server.<br><br>It is used like other init scripts, with start or stop modifiers. For example, to stop the service, you would enter /etc/init.d/ndsd stop.<br><br>To start the service, you would enter: /etc/init.d/ndsd start. |