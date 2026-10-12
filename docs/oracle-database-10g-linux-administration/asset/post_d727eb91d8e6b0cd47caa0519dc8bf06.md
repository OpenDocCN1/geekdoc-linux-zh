
## Migrating the Application Tier

Migrating the application tier involves the movement and reconfiguration of the application data files. This involves a lot of copying of data and running AutoConfig to reconfigure the application layer as well as the metadata. This should be done with great care and diligence, since it can be difficult to fix things that have been misconfigured.

## Migrating Using the Linux Platform Migration Tool

Linux Platform Migration provides a way to easily move just an existing E-Business Suite middle-tier system (not the database tier) from any platform to Linux, allowing you to use fast, low-cost Linux hardware. The migration utility retains your exact applications patch level so that no APPL_TOP/Database synchronization is necessary. It also allows you to retain many customizations. Instead of installing the E-Business Suite from scratch as outlined previously in this chapter, you would do the following:

- 1. Prepare the existing system for migration, such as to implement AutoConfig (if on R11.5.8 or earlier). Create and export a current view global snapshot to a text file.
- 2. Prepare the new system for migration, including applying OS patches, installing Perl and JDK, and setting Linux Kernel parameters (refer to “Installing Oracle Applications: A Guide to Using Rapid Install”).
- 3. Apply the Platform Migration utility patch to the source system. This step creates a custom upload file that is sent to Oracle. Oracle will then create a custom patch that will later be applied. Oracle usually returns this patch very quickly (in a matter of days).
- 4. Generate and upload the manifest of customer-specific files on the source system.
- 5. Copy specific middle-tier files from the source to the target system (APPL_TOP, OA_HTML, OA_JAVA, COMMON_TOP/util and COMMON_TOP/_pages, identitydb.obj).
- 6. Clone the AutoConfig XML application context file.
- 7. Install the middle-tier technology stack (using rapidwiz) on the target system.
- 8. Apply the Oracle Interoperability patches for Red Hat (if running this flavor of Linux) to the target system.
- 9. Run the AutoConfig Setup phase on the target system with the cloned context file.
- 10. Download and apply the customer-specific update with AutoPatch on the target system.
- 11. Apply the patch on the target system for migrating from Windows that contains Linux-specific APPL_TOP files that don't exist on Windows.
- 12. Apply any missing technology stack patches previously applied to your system but not included in new techstack installation.
- 13. Apply the latest techstack interop patch to the new applications file system.
- 14. Regenerate file system objects (adgensn.sh), and then run adadmin to regenerate messages, forms, reports, graphics, and JAR files.
- 15. Run AutoConfig to complete target system configuration.
- 16. Perform Finishing Tasks (update third-party extensions; recompile custom code; perform required tasks for UTF8, Discoverer 4i, SSO, and Portal; update with new printer and Workflow configuration settings; start all services).

Once the application layer has been moved and the metadata repository has been configured, if you are migrating the database tier to Linux as well, it is time to move the actual data, as is described in the next section.

## Migrating the Database Tier

The migration of the database tier involves running a patch at the database on the system that you are migrating from, performing an export, and then importing that data into the target system. The procedure for exporting and importing the data into the new system will vary slightly, depending on whether you are exporting data from an Oracle8i database, an Oracle9i database, or an Oracle10g database. Even the latest version of the Oracle E-Business Suite can utilize an Oracle 9.2 or Oracle 10g database (though the application tier still utilizes Oracle 8.0.6 executables). Again, these are the basic steps:

- 1. Apply the pre-export patch. This patch prepares the database for export. You must perform this step before performing the export or the import will not be successful.
- 2. Export the database.
- 3. Copy the export file(s) to the new system.
- 4. Run the post-import steps. These steps will be described in the interoperability notes.

While migrating the database tier, it is a good time to optimize your database layout and I/O subsystem. Since export and import are going to be used, the underlying data structures of the Oracle database can be modified. If you are not already using them, convert to locally managed tablespaces. If necessary, you can expand tablespaces to span multiple data files. Since the default Oracle E-Business Suite installation as of Release 11.5.10 now creates only 12 consolidated tablespaces with the new Oracle Applications Tablespace Model (OATM), whereas older versions included over one hundred tablespaces (two for each module; one for data, one for indexes, plus some extras), this is also a good time to migrate to the OATM.

![](img/9479df2d00f5e62b87366b125224950f_483_0.png)

**NOTE**
The AutoConfig utility not only configures the application programs but configures the metadata in the database as well. This is important to keep in mind, since a mistake could mean that you need to spend significant time deleting data from the database.

As you can see, there are numerous steps that must be completed for a successful migration. If you have not already done one of these, make sure you are aware of all of the steps required before beginning the migration.

## Converting the Database Tier to RAC

Converting the database tier to a RAC cluster is a multiphase project. During the migration or the initial installation of the E-Business Suite, the Oracle database is created. You should not skip this step, since the rapid installer creates the necessary tablespaces and structures that are needed. In order to convert the database tier to RAC, another Oracle installation must be done with the RAC option and the E-Business Suite database must be moved to the new Oracle home. This is due to the fact that the Oracle installer will configure additional components in a RAC environment that are not present in a non-RAC installation. In order for these components to be installed, the Oracle Cluster Ready Services must be running at installation time. The steps are as follows:

- 1. Install the Oracle instance using the rapid installer as part of the E-Business Suite installation or migration.
- 2. Install an Oracle RAC cluster.
- 3. Move the E-Business Suite database to the RAC cluster.
- 4. Set up Parallel Concurrent Processing (PCP).

These steps are fairly straightforward, but they are time-consuming to perform and require a great deal of attention to detail (and sometimes some debugging skills). The entire process of converting the database to RAC and setting up PCP requires planning and a good check list.

## Testing

One of the most important steps in migrating the Oracle E-Business Suite to Linux is the testing phase. Once everything has been configured and all of the data has been migrated, you must perform rigorous functional and performance tests to make sure everything has been properly configured. In addition, it is a good idea to compare row object counts in the new database to those of the original database as it was when the export was done. Carefully check all of the import logs and the Oracle alert log for errors.

Once the testing has been completed, you will be ready for the final conversion and the utilization of the new system by the user community. At this point, the system should be carefully monitored for the next few weeks. Once this has been completed, normal monitoring schedules can be used.

## Summary

This chapter has served as an introduction and an overview of how to install, configure, and migrate the Oracle E-Business Suite to Linux. Because the Oracle E-Business Suite is an extremely complicated product, this chapter is not an instruction guide to how to install and configure it, but rather an introduction to setting it up on Linux. Linux is an ideal platform for the Oracle E-Business Suite because of the flexibility, performance, and industry-wide support for Linux. In fact, Oracle itself has adopted Linux as the platform of choice for running its own business.

The Linux platform is rapidly growing in popularity and has been adopted by not only the user community but the hardware and software development community as well. Linux has proved itself to be an ideal platform for web servers, application servers, firewalls, and domain name servers, as well as database servers. The Oracle Application Server and E-Business Suite run very well on the Linux platform. As Linux matures, so will Linux be adopted as the enterprise platform of choice.
