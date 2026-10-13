If a system isn't already registered, the following steps supports registration of an RHEL 6 system from the command line:

+   1. Run rhn_register from the command line. If the system is already registered, you're prompted with the opportunity to leave the registration process.
+   2. You'll see a screen related to the configuration of software updates. The exact wording varies, depending on whether the registration is proceeding at the console or the GUI. If you need more information about the RHN, select Why Should I Connect To RHN; otherwise, select Next or Forward to continue. (Next is the option in the console; Forward is the option in the GUI.)
+   3. In the GUI version, you'll see options associated with the RHN Proxy and Satellite servers. The console version of the registration tool skips this step.
+   4. You'll see a screen where you can enter RHN login information. Do so and select Next or Forward to continue.
+   5. Now choose whether to register a system profile and whether to send basic hardware information about your system; make appropriate decisions and select Next or Forward to continue.
+   6. Next, choose to include a list of installed packages, which helps the RHN check whether you need software and security updates. Make any desired changes and select Next or Forward to continue.
+   7. Finally, choose whether to send your system profile to the RHN. If you click Cancel, the tool stops, and your system is not registered. If you want to register, select Next or Forward to continue.
+   8. Your system attempts to contact the RHN server (or possibly your RHN Satellite Server). If a free subscription entitlement is available, a message eventually appears that the system is successfully registered with the RHN.

# CERTIFICATION SUMMARY

This chapter focuses on the management of RPM packages. With different switches, you also looked at how the rpm command installs, removes, and upgrade packages, as well as how it works locally and remotely. When presented with a new version of a kernel, it's important to never "upgrade." A properly configured installation of a later kernel version does not overwrite, but brings kernels together, side by side. You'll then be able to boot into either kernel.