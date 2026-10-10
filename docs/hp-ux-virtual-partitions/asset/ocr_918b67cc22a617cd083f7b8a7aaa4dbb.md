```
Preview only. Tape not created
The /var/opt/ignite/recovery/arch.include file has been created.
This can be modified to exclude known files.
Only delete files or directories that are strictly user created.
The creation of the System Recovery tape can then be
resumed using the -r option.
No further checks will be performed by the commands.
Cleanup
```

The **arch.include** file has been produced at this point. This file lists the
files that will be part of the archive that you can modify. The following is an
abbreviated listing of **arch.include**, showing just the very beginning and
very end of the file:

```
/lost+found
/etc
/etc/vue
/etc/vue/config
/etc/vue/config/types
/etc/vue/config/types/tools
/etc/vue/config/types/tools/System_Admin
/etc/vue/config/types/tools/System_Admin/FontClientSvr
/etc/vue/config/types/tools/System_Admin/SetNetworking
/etc/vue/config/types/tools/System_Admin/ShutdownSystem
/etc/vue/config/types/tools/System_Admin/VerifyPRX
/etc/vue/config/types/tools/System_Admin/VerifyPRX
/etc/vue/config/types/tools/Media
.
.
.
/spp/scripts/tc_standalone
/spp/scripts/sppconsole.old
/spp/unsupported
/spp/unsupported/chus
/spp/unsupported/clear_pid
/spp/unsupported/ex_shm
/spp/unsupported/rdr_dumper.fw
/spp/unsupported/rdr_formatter
/spp/unsupported/reset_jtag
/spp/unsupported/scan_sram
/users
/users/sppuser
/users/sppuser/.Xdafaults
/users/sppuser/.cshrc
/users/sppuser/.kshrc
/users/sppuser/.login
```