# # Graphical Performance Tuning Tools

**O**racle provides several *Graphical User Interface (GUI)* database management tools that can be used to aid a tuning effort. These GUI tools are divided into three product categories:

+   - Oracle Enterprise Manager Console
+   - Oracle Diagnostics Pack
+   - Oracle Tuning Pack

The Oracle Enterprise Manager Console is included with the basic *Oracle9i* database software. The Diagnostics and Tuning Packs are extra-cost options that require a separate license with Oracle. Each of these GUI tools is discussed briefly in the following section. Additional details about some of these GUI tools also appear in relevant sections of sub-sequent chapters.

> **NOTE** Free evaluation copies of Oracle’s Diagnostic and Tuning Packs can be downloaded from <http://technet.oracle.com/software/products/oem/content.html>.

**Oracle Objective**: Collect statistics using Enterprise Manager

# ## Oracle Enterprise Manager Console

*Oracle Enterprise Manager (OEM)* is the core of Oracle’s GUI database management tools. The OEM Console includes several tools designed to help you graphically monitor and manage your databases. Figure 2.6 shows a picture of the OEM Console for *Oracle9i*.

The OEM Console seamlessly integrates components of the *DBA Management*, *Tuning*, and *Diagnostic Packs* into one centralized GUI environment from which you can administer all your databases. The base OEM product is made up of six management tools. These tools and their uses are summarized in Table 2.6.

A critical component in the OEM architecture is the *Oracle Intelligent Agent*. This autonomous OS process allows the OEM Console to perform a variety of tasks against the databases that the Console is managing.