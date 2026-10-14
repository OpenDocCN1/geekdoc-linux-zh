![](bbox=[0.084, 0.078, 0.918, 0.331])

Please note that as *TruCluster Server* version 5.1A is the latest version, we have yet to test the Update Installation to a later version of *TruCluster Server*.

# 25.5.2.3　Setup Stage for a New Hardware Delivery (NHD)⁶

As of this writing, not much has been documented on what is required for performing a rolling upgrade of a cluster for a New Hardware Delivery. Based on available information, when a rolling upgrade for an NHD Installation is performed, at the Setup Stage, the NHD installation kit is copied from its source media to `/var/adm/update/NHDKit` for accessibility during the Install Stage. For more information on the New Hardware Delivery kit, please see Compaq’s *Tru64 UNIX New Hardware Delivery Release Notes and Installation Instructions* when this document becomes available.

# 25.5.2.4　Setup Stage for Installation of a Patch Kit

Unlike the Setup Stage for either an Update Installation or an NHD Installation, the Setup Stage for a Patch Kit does not do anything additional in terms of copying files for greater accessibility.

Again, if your existing cluster is at *TruCluster Server* version 5.0A or at *TruCluster Server* version 5.1, you will see a slightly different version of output from the “`clu_upgrade setup 1`” command than if you were using *TruCluster Server* version 5.1A.

The following sample output of “`clu_upgrade setup 1`” command comes from a *TruCluster Server* version 5.1 system:

> ⁶ This is a feature of *TruCluster Server* version 5.1A or later.