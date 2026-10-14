**NOTE**

You can find the man page documents for the non-X terminal version of YaST under the `yast2` man pages.

SuSEconfig and YaST are tools bundled with SLES that help you configure and maintain your server. Together, the utilities provide a consistent approach and reduce the chances of a forgotten step when multiple changes are required. Now that you have a basic understanding of the YaST tool, it is time to apply this knowledge to everyday system management.

# ## Adding and Removing Packages

Proper maintenance of the different modules that reside on your system helps ensure the reliability of the services you offer. An important step in the configuration of a server is to ensure that only required packages are installed on a system. This has the dual benefit of minimizing resources consumed as well as reducing the possible exposure to exploits in unused packages that tend to be forgotten and therefore not adequately maintained.

How do you know what minimal subcomponents are required to support the main tasking of your server? As a first approximation, this is handled for you by the YaST utility. YaST and the underlying system maintain a list of interdependencies between different packages. If an attempt is made to install or remove a component that is required by a module you need, YaST will warn you.

# ### Installing a Package

The process of adding and removing packages using YaST is fairly simple. As an example, the following walks through the creation of a Domain Name Services (DNS) server. The first step is to build an SLES server and then install the DNS software. Configuring the DNS service is somewhat more complicated and will be covered in Chapter 8, “Network Services.”

Continuing with the desire to run only applications that are absolutely necessary, install a server with SLES and choose to install a minimum system. This installs SLES, YaST, and a number of other utilities that make the system easier to administer. To convert this base system into a DNS server, you must add the DNS server software (Bind).

Because the newly installed system is running a base install of SLES, the X Windows System is not available. Sign on to the machine using the root account and start YaST by typing yast at the command line. Figure 2.1 shows the