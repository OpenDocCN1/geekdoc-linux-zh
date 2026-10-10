# 5) Virtual Partition Kernel-Related Work

Each Virtual Partition has its own instance of HP-UX 11i, which has its own HP-UX kernel. It is likely that you’ll customize these kernels in a variety of ways to suit the applications you have running in the respective vPars. When you install the vPars software, it automatically reconfigures the kernel to include the vPar drivers and make the kernel relocatable. You do not have to perform the kernel-related steps in this section because they are performed for you when vPars software is loaded. It is still informative; however, to see the steps that were manually performed in this section to get better insight concerning the way vPars operate. In this step we’ll investigate the files that have been updated by the vPars application and build the new kernel. Keep in mind that the new kernel needs to be built on every volume that has HP-UX 11i on it and will run a vPar.

Because memory is shared among multiple vPars, the kernel must be relocatable in memory. At the time of this writing, there are patches that allow the kernel to be built as a relocatable kernel. We won’t perform any checks related to patches.

The file /sbin/vrecheck is a vPar file that is required on the system. The following listing is a portion of /usr/conf/gen/config.sys that checks to see if /sbin/vrecheck has been loaded on the system:

```
# Determine whether the linker supports kernel relocation.  [:::d::d]
# Link the kernel using the relocation options.
LOADOPTS_ADDL=`
        if [ -f /sbin/vrecheck ]; then  \
            $(WRK)/$(IZ) \
            $(AWK) '$$0 == "92453-7 linker" { \
                if ( vers[1] == "9" 66 \
                    { [ vers[2] == 11 66 vers[3] >= 25 ] ] || vers[2] > 11 } \
                        print "${LOADOPTS_RELOC}"; \
                    else print "${LOADOPTS_STATIC}"; }
            fi;`
```

The following is a long listing of /sbin/vrecheck which was loaded with the vPar software: