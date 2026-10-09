device options tdfxdrm viadrn DRM_DEBUG 3dfx Voodoo 3/4/5 and Banshee VIA # Include debug printfs (slow)

Are you using any of these video cards on your desktop? Maybe you want a custom kernel that includes the appropriate device driver.

If the *NOTES* file lists all the features for every possible device, why not just use it as the basis for your kernel? First, such a kernel would use up far more memory than the GENERIC kernel. While even small modern machines have enough memory to run GENERIC without trouble, if the kernel becomes ten times larger without the corresponding increase in functionality, people would get annoyed. Also, many options are mutually exclusive. You'll find options that let you dictate how the kernel schedules processes, for example. The kernel can use only one scheduler at a time, and each scheduler runs its tendrils throughout the kernel. Adding all of them to the kernel simultaneously would increase code complexity and decrease stability.

I make it a point to review *NOTES* every release or two, just to look for interesting new features.

# Inclusions and Exclusions

FreeBSD's kernel configuration has two interesting abilities that can make maintaining a kernel easier: the no options and the include feature.

The `include` feature lets you pull a separate file into the kernel configuration. For example, if you have a kernel configuration that can be described as "GENERIC with a couple extra tidbits," you could include the GENERIC kernel configuration with an `include` statement:

```
include GENERIC
```

So, if you want to build a kernel that has all the functionality of GENERIC but also supports the DRM features of the VIA 3d chips, you could create a valid kernel configuration composed entirely of the following:

ident VIADR M include GENERIC