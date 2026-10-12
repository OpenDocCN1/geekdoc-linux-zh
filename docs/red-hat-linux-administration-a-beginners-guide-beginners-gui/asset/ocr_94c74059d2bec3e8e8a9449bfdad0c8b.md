a simple password file. And why not? It does what we want. Most users understand the need for it, and it’s a well-tested method to get the job done. However, some sites have needed to expand on this.

A popular example of exceptions to the rule is still password-based, but instead of using standard UNIX passwords, another method of storing passwords was needed. For some sites, this is based on a database, thereby allowing for a larger number of users. For others, it is adapting to an existing system (like an NT server acting as a PDC).

This section describes how PAM is set up under Red Hat Linux. The placement of files may not be exactly the same in every other distribution, but the underlying configuration files and concepts still apply.

# ## How PAM Works

PAM is to other programs as a DLL is to a Windows application—it is just a library. When programs need to perform authentication on someone, they call a function that exists in the PAM library.

When invoked, PAM checks the configuration file for that application. If there isn’t a configuration file, it uses a default configuration file. This configuration file tells the library what types of checks need to be done in order to authenticate the user. Based on this, the appropriate module is called on. (Red Hat folks can see these modules in the /lib/security directory.)

This module can check any number of things. It can simply check the /etc/passwd file or the /etc/shadow file, or it can perform a more complex check like calling on a LDAP server.

> **NOTE**
> The PAM web site (http://www.kernel.org/pub/linux/libs/pam/) offers a complete list of available modules.

Once the module has made the determination, an “authenticated/not authenticated” message is passed back to the calling application.

If this feels like a lot of steps for what should be a simple check, you’re almost correct. While it feels like a lot of steps, each module here is very small and does its work very quickly. From a user’s point of view, there should be no noticeable performance difference between an application that uses PAM and one that does not. From a system administrator’s and developer’s point of view, the flexibility this scheme offers is incredible and a very welcome addition.

# ## PAM’s Files and Their Locations

On a Red Hat–style installation, PAM puts her configuration files in certain places. These file locations and their definitions are listed in Table 5-3.

Looking at the list of file locations in Table 5-3, one has to ask why PAM needs so many different configuration files. “One configuration file per application? That seems crazy!”