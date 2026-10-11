```
```
gpg: Good signature from "Linux Kernel Archives Verification Key <ftpadmin@kernel.org>"
gpg:    aka "Linux Kernel Archives Verification Key
<ftpadmin@kernel.org>"
```
```

> If you see a warning about trust path issues, you can safely ignore it. This is per the kernel.org instructions, which can be found at http://www.kernel.org/signature.html.

> You will likely see questions about the gpg signature or the md5 checksum being used to validate kernel source code. Download the associated files and read the man pages to ensure you understand what we've covered.

# Configuring the Kernel

There are three main methods for determining what is included or excluded in the new kernel you are about to compile. The following commands are run in the top-level directory of the kernel source code, and each of the options is an argument to the make command:

+   *   make config—Contains a lot of yes/no questions. This is a text-based, very simple and painful way to configure the kernel because errors cause you to restart the process.
+       *   make menuconfig—Contains a text-based menu of options that's surprisingly easy to navigate.
+       *   make xconfig—X-based and GUI, this is the one for the recovering MCSE crowd, or the aesthetically oriented folks.

> I won't discuss the make config option in any detail because it's obsolete and its functionality is encompassed entirely by friendlier utilities.

# make menuconfig

When configuring the options for what will or won't be in the compiled kernel, it's important to know what the little brackets and characters mean. Particularly, this is important in the menuconfig command, shown in Figure 14.2.