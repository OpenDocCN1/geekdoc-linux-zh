# ## Objective 5

# ## Manage Xen Domains at the Command Line

In the following you learn how to manage Xen domains at the command line. This includes:

+   - Understand a Domain Configuration File
+   - Use the xm Tool
+   - Automate Domain Startup and Shutdown

# ### Understand a Domain Configuration File

Every Xen domain needs a configuration file. For domains which have been created with YaST, the configuration file is usually located in /etc/xen/vm/.

Under /etc/xen/examples, you find two example files, which can be used if you would like to create a configuration from scratch.

+   - **xmexample1**. This is a template configuration file for a single domain.
+   - **xmexample2**. This is an example for multiple domain configurations in one file.

For the beginning, **xmexample1** is a better choice.