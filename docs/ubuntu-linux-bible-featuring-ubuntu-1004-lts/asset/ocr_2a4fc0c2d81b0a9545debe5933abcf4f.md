# Part I: Getting Started with Ubuntu

This option is rarely necessary on a server installation, since the system should be physically secure and the object of this option is to protect the administrative account from access by other users of the system (which should be none on a server system). To secure this file volume, press Tab twice to select Yes, and then press Return. To skip creating an encrypted home directory for the specified user, make sure that the default value of No is selected, and press Return.

+   16. The dialog shown in Figure 3-15 prompts you to the location of any HTTP proxy that you need to use in order to access the Internet to download packages. If you need to use an HTTP proxy, enter its URL in this dialog. If you do not need to use an HTTP proxy, leave this field empty and press Return to proceed.

![](bbox=[0.105, 0.325, 0.975, 0.66])

+   17. The installer installs and configures several packages based on your selections up to this point. Next, the dialog shown in Figure 3-16, which enables you to specify whether the system should not download updates automatically, should download updates automatically, or should use Landscape to manage the system. (Landscape is a Web-based system management and monitoring system that is available from Canonical. For more information about Landscape, see www.canonical.com/projects/landscape)

I typically leave this to the default value, No Automatic updates, because it's good policy to only update servers when necessary — it's more important to know exactly what's running on your servers to always be up-to-date (though it's equally good practice to check for security-related updates frequently).

76