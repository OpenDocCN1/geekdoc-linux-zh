installed. However, if you specify the **-d** command-line argument on the **patchadd** command, the files are not backed up, and the patch cannot be removed.

The default backup directories, located under /var/sadm/pkg, are based on the installed package or packages being modified by the patch and the patch number. For example, the x86 find command patch (110906-01) modified the SUNWcsu package. Any files changed by installing this patch will be saved under the /var/sadm/pkg/SUNWcsu/110906-01 directory. You can specify a different backup directory by using the **-B** command-line argument.

The **patchadd** command will fail if any of the following occur:

+   - A package being patched is not installed or is only partially installed.
+   - The patch requires another patch that is not installed.
+   - The patch is incompatible with another patch already installed.
+   - The current version or a higher version of the patch is already installed.
+   - The architecture of the patch and the system do not match.

![](bbox=[0.141, 0.5, 0.889, 0.584])

# Determining Which Patches Are Installed

Two commands can be used to generate a list of installed patches for a stand-alone system:

+   - **showrev -p**
+   - **patchadd -p**

Both commands generate almost identical lists. The following example illustrates the use of the **showrev(1M)** command (the output is formatted for readability):

```
```text
$ showrev -p
Patch: 110906-01
Obsoletes:
Requires:
Incompatibles:
Packages: SUNWcsu
Patch: 108632-06
Obsoletes:
```
```