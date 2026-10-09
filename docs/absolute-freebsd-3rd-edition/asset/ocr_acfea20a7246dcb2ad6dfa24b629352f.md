After a few upgrades, you'll find that you'll never fall back to some of the existing boot environments. Once I upgrade this host to, say, 12.2-RELEASE-p29, chances are I'll never ever reboot into 11.0-p11 again. Remove obsolete boot environments and free up their disk space with `beadm destroy`.

```
# beadm destroy 11.0-p11
Are you sure you want to destroy '11.0-p11'?
This action cannot be undone (y/[n]): y
Destroyed successfully
```

Answer `y` when prompted, and beadm will remove the boot environment.

# ### Boot Environments at Boot

So you've truly hosed your operating system. Forget getting to multiuser mode, you can't even hit *single-user* mode without generating a spew of bizarre error messages. You can select a boot environment right at the loader prompt. This requires console access, but so would any other method of rescuing yourself.

The boot loader menu includes an option to select a boot environment. Choose that option. You'll get a new menu listing every boot environment on the host by name. Choose your new boot environment and hit `ENTER`. The system will boot into that environment, giving you a chance to figure out why everything went sideways.

# ### Boot Environments and Applications

It's not enough that your upgrade failed. It might take your application data with it.

Most applications store their data somewhere in the root dataset. MySQL uses `/var/db/mysql`, while Apache uses `/usr/local/www`. This means that falling back to an earlier boot environment can revert your application data with the environment. Depending on your application, you might want that reversion—or not.