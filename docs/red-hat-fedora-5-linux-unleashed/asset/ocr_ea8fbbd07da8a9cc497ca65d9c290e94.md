# **USING THE PATCH COMMAND**

If you have a special, nonstandard patch to apply—such as a third-party patch for a commercial graphic card, for example—you can use the `caton` command rather than the special patch-kernel script that is normally used for kernel source updates. Here are some quick steps and an alternate method of creating patched code and leaving the original code alone.

+   1. Create a directory in your home directory and name it something meaningful, like `~/mylinux`.
+   2. Copy the pristine Linux source code there with
+      ```
+      $ tar xzjf /usr/src/linux-2.4.25.tar.gz -C ~/mylinux
+      ```
+   3. Copy the patch file to that same directory with
+      ```
+      $ cp /path/to/file.patch ~/mylinux
+      ```
+   4. Change to the `~/mylinux` directory with
+      ```
+      $ cd ~/mylinux
+      ```
+   5. Apply the patch with
+      ```
+      $ cat file.patch | patch -p1 > mypatch.log 2>&1
+      ```
+      (This last bit of code saves the message output to a file so that you can look at it later.)
+   6. If the patch applies successfully, you are done and have not endangered any of the pristine source code. In case the newly patched code does not work, you will not have to reinstall the original, pristine source code.
+   7. Copy your new code to `/usr/src/kernels` and make that special symbolic link described elsewhere in the chapter.

# ### Compiling the Kernel

If you want to update the kernel from new source code you have downloaded or you have applied a patch to add new functionality or hardware support, you will have to compile and install a new kernel to actually use that new functionality. Compiling the kernel involves translating the kernel's contents from human-readable code to binary form. Installing the kernel involves putting all the compiled files where they belong in /boot and /lib and making changes to the bootloader.

The process of compiling the kernel is almost completely automated by the make utility, as is the process of installing. By providing the necessary arguments and following the steps covered next, you can recompile and install a custom kernel for your use.

Here is a checklist of steps to compile and configure the kernel:

+   1. Verify a working bootdisk for the old kernel to be able to reboot your system in case something goes wrong with the new kernel.