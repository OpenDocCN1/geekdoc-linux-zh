However, in case of failure the module gives immediate feedback to the user and no further modules are processed.

You can use the requisite flag as a basic filter, checking for the existence of certain conditions that are essential for a correct authentication.

+   - **optional.** The failure or success of a module with this flag does not have any direct consequences.
+   You can use this flag for modules that are only intended to display a message (such as telling a user that mail has arrived) without taking any further action.

+   - **sufficient.** After a module with this flag has been successfully processed, the calling application receives an immediate message about the success and no further modules are processed (provided there was no preceding failure of a module with the "required" flag).
+   The failure of a module with the sufficient flag has no direct consequences. In other words, any subsequent modules are processed in their respective order.

+   - **include.** This is not really a control flag but indicates that the keyword in the next column is to be interpreted as a file name relative to /etc/pam.d/ that should be included at this point.
+   The file included has to have the same structure as any other PAM configuration file.
+   The purpose of **include** files is to simplify changes concerning several applications.

+   - **Module.** The PAM modules are located in the directory `/lib/security/`. Every filename of a module starts with the prefix `pam_`. You do not need to include the path, as long as the module is located in the default directory `/lib/security/`.

> For all 64 bit platforms supported by SUSE Linux, the default directory is /lib64/security/.

![](bbox=[0.22, 0.88, 0.28, 0.92])