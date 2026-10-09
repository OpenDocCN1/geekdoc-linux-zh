Kernel” (page 577) explains how to create a default version of this file if it does not exist and how to edit the file if it does exist.

# ## REPLACING A CUSTOM KERNEL

If you have already configured a custom kernel, you may want to replace it with a similarly configured, newer kernel. Each kernel potentially has new configuration options, however—which explains why it is poor practice to use an old **.config** file for compiling a new kernel. This section explains how to upgrade an existing **.config** file so it includes options that are new to the new kernel and maintains the existing configuration for the old options.

Work in the directory you downloaded or extracted the source code to. The system keeps a copy of the configuration file for the kernel the local system is running in /boot. The following command copies this file to **.config** in the working directory:

```
$ cp /boot/config-$(uname -r) .config
```

In this command, the shell executes **uname -r** and replaces **$(uname -r)** with the output of the command, which is the name of the release of the kernel running on the local system. For more information refer to “Command Substitution” on page 362.

Next give the command **make oldconfig** to patch the **.config** file with options from the new kernel that are not present in the old kernel. This command displays each kernel option that is the same in the new and old kernels and automatically sets the state of the option in the new kernel the same way it was set in the old kernel. It stops when it finds an option that appears in the new kernel but not in the old kernel. It then displays a prompt, which is similar to [N/y/?] (NEW), showing possible responses and indicating this option is new. The prompt shows the default response as an uppercase letter; you can type this letter (uppercase or lowercase) and press RETURN, or just press RETURN to select this response. In the example, the Tickless System option is new and the default response is Y for yes. include the option in the new kernel. To select a nondefault response (n means no, do not include the option and m means include the option as a module), you must type the letter and press RETURN. Enter ? followed by RETURN to display more information about the option.

```
```
$ make oldconfig
scripts/kconfig/conf -o arch/i386/Kconfig

* Linux Kernel Configuration
*
*
* Code maturity level options
*
* Prompt for development and/or incomplete code/drivers (EXPERIMENTAL) [Y/n/?] y
*
* General setup
* ```


```