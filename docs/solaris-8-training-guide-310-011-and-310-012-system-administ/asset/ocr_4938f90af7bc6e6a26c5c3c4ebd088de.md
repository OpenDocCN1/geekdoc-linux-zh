# Other Source Files

The following files can also be copied to the /var/yp directory to be used as source files for NIS maps, but first be sure that they reflect an up-to-date picture of your system environment:

+   - auto.home or auto_home
- auto.master or auto_master
- bootparams
- ethers
- netgroup
- netmasks
- networks
- protocols
- rpc
- services
- shadow

Unlike other source files, the /etc/mail/aliases file cannot be moved to another directory. This file must reside in the /etc/mail directory. Be sure that the /etc/mail/aliases source file is complete by verifying that it contains all the mail aliases that you want to have available throughout the domain.

# Preparing the Makefile

After checking the source files and copying them into the source file directory, you need to convert those source files into the ndbm format maps that the NIS service uses. This is done automatically for you by ypinit. I describe how to set up ypinit in the next section.

The ypinit script calls the program make, which uses the Makefile located in the /var/yp directory. A default Makefile is provided for you in this directory. It contains the commands needed to transform the source files into the desired ndbm format maps.