# In Sum 135

FEATURE(`blacklist_recipients`)`dnl
FEATURE(`redirect`)`dnl
FEATURE(`use_cw_file`)`dnl
EXPOSED_USER(`root`)

The redhat11.mc macro control file has been reduced to a more readable seven lines. The OSTYPE command was edited to call the new redhat7.0.m4 OSTYPE source file and the DOMAIN command was added to call the new foobis.m4 DOMAIN source file. These three files combine all of the desirable features that we saw in the generic-linux.mc configuration and in the redhat.mc configuration.

# In Sum

A Sendmail configuration is not built from scratch. Start from one of the sample files that is provided as part of the Sendmail source code distribution or start with the configuration file that comes from your distribution vendor. Read and understand the vendor's configuration before modifying it to create your own. Dont vendor often make compromises to create a configuration that runs on a wide variety of systems. Focus the configuration you create on those capabilities that you actually need.

Starting from a sample configuration can simplify the creation of your configuration, but the sample configurations carry their own level of complexity. Some, like generic-linux.mc, are reasonably simple, but may not provide the features you need. Others, like redhat.mc, are more complex than necessary. The way to attack the complexity of the sample configuration files is one line at a time. Even a very large macro configuration file has fewer than 30 lines. Using a reference, as this book, get a general idea of what each line does. Discard those lines that are unnecessary for your configuration. Then research the others in more detail to select those that you want to keep.

The analysis of the configurations in this chapter has shown that Sendmail relies heavily on database files to route mail, convert addresses, and control spam. In the next chapter, we look at the databases used by Sendmail and describe how you can use those databases to configure your system.