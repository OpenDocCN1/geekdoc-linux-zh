# Migrating the Application Tier

Migrating the application tier involves the movement and reconfiguration of the application data files. This involves a lot of copying of data and running AutoConfig to reconfigure the application layer as well as the metadata. This should be done with great care and diligence, since it can be difficult to fix things that have been misconfigured.

# Migrating Using the Linux Platform Migration Tool

Linux Platform Migration provides a way to easily move just an existing E-Business Suite middle-tier system (not the database tier) from any platform to Linux, allowing you to use fast, low-cost Linux hardware. The migration utility retains your exact applications patch level so that no APPL_TOP/Database synchronization is necessary. It also allows you to retain many customizations. Instead of installing the E-Business Suite from scratch as outlined previously in this chapter, you would do the following:

+   1. Prepare the existing system for migration, such as to implement AutoConfig (if on R11.5.8 or earlier). Create and export a current view global snapshot to a text file.
+   2. Prepare the new system for migration, including applying OS patches, installing Perl and JDK, and setting Linux Kernel parameters (refer to “Installing Oracle Applications: A Guide to Using Rapid Install”).
+   3. Apply the Platform Migration utility patch to the source system. This step creates a custom upload file that is sent to Oracle. Oracle will then create a custom patch that will later be applied. Oracle usually returns this patch very quickly (in a matter of days).
+   4. Generate and upload the manifest of customer-specific files on the source system.
+   5. Copy specific middle-tier files from the source to the target system (APPL_TOP, OA_HTML, OA_JAVA, COMMON_TOP/util and COMMON_TOP/_pages, identitydb.obj).
+   6. Clone the AutoConfig XML application context file.
+   7. Install the middle-tier technology stack (using rapidwiz) on the target system.
+   8. Apply the Oracle Interoperability patches for Red Hat (if running this flavor of Linux) to the target system.
+   9. Run the AutoConfig Setup phase on the target system with the cloned context file.