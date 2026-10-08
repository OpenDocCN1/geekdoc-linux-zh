Upon entering the chroot environment in Chapter 6, the first major package to be installed is Glibc, due to its self-sufficient nature mentioned above. Once Glibc is installed into /usr, we will perform a quick changeover of the toolchain enables, and then proceed in building the rest of the target LFS system.

# 5.3. General Compilation Instructions

When building packages there are several assumptions made under the instructions:

+   - Several of the packages are patched before compilation, but only when the patch is needed to circumvent a problem. A patch is needed in both this and the next chapter, but sometimes in one or the other. Therefore, do not be concerned if instructions for a downloaded patch seem to be missing. Warning messages about offset or fuzz may also be encountered when applying a patch. Do not worry about these warnings, as the patch was still successfully applied.
- During the compilation of most packages, there will be several warnings that scroll by the screen. These are normal and can be safely ignored. These warnings are as they appear—warnings about deprecated, but not invalid, the use of the C or C++ standards. C standards change fairly often, and some packages still use the older standard. This is not a problem, but does prompt the warning.
- Check one last time that the `LFS` environment variable is set properly:

```
echo $LFS
```

Make sure the output shows the path to the LFS partition's mount point, which is `/mnt/lfs`, using our example.
- Two important items must be emphasized:

> **Important**
The build instructions assume that the Host System Requirements, including symbolic links, have been set properly:
- bash is the shell in use.
- sh is a symbolic link to bash**.
- /usr/bin/awk is a symbolic link to gawk.
- /usr/bin/yacc is a symbolic link to bison or a small script that executes bison.

> **Important**
To-emphasize the build process:
1. Place all the sources and patches in a directory that will be accessible from the chroot environment such as `/mnt/lfs/sources/`. Do not put sources in `/mnt/lfs/tools/`.
2. Change to the sources directory.
3. For each package:
a. Using the tar program, extract the package to be built. In Chapter 5, ensure you are the lfs user when extracting the package.
b. Change to the directory created when the package was extracted.
c. Follow the book's instructions for building the package.
d. Delete the extracted source directory unless instructed otherwise.