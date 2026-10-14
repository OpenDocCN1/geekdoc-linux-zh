

options you would use for a DHCP install with the static settings, except comment out or remove the disable_dhcp option. Finally, add the following options to the preseed:

```
d-i netcfg/dhcp_failed note
d-i netcfg/dhcp_options select Configure network manually
```

With these options in place, on networks where DHCP works, the install will use those settings. In case DHCP fails, the installer will then fall back to your static settings.

## Partitioning

As you saw in the installation chapter (Chapter 1), there are many different ways to partition an Ubuntu server, and so it should be no surprise that there are also many preseeding options for partitioning. First, let’s break down the options I used in my default preseed.cfg:

```
d-i partman-auto/method string regular
d-i partman-auto/purge_lvm_from_device boolean true
d-i partman-lvm/confirm boolean true
d-i partman-auto/choose_recipe select atomic
d-i partman/confirm_write_new_label boolean true
d-i partman/choose_partition select finish
d-i partman/confirm boolean true
```

With these options, the installer will simply select the first available disk it can find and then overwrite it with one big / partition and a swap partition. For something so basic it certainly took quite a few options, so let’s go through these options one by one and discuss what part they play.

- **partman-auto/method**
  This option defines what partitioning method to use for the automatic partitioning and can accept the options regular, lvm, or crypto. As the options suggest, the latter two set up partitions as LVM or encrypted volumes.

- **partman-auto/purge_lvm_from_device and partman-lvm/confirm**
  These options just save you from having to acknowledge warning prompts in the installer. The former option will purge any old LVM configuration from the disk if it exists, and the latter confirms writing any LVM partitions you may have set up.

- **partman-auto/choose_recipe**
  The Ubuntu partition program allows a few different predefined partitioning recipes from which the user can choose. The atomic recipe sets up everything on a single partition. If you set the option to `home`, it will separate out a `/home` partition as well, and if you set it to `multi`, you will get separate `/home`, `/usr`, `/var`, and `/tmp` partitions.

- **partman/confirm_write_new_label, partman/choose_partition, and partman/confirm**
  These are more options that tell the installer to proceed with partitioning without extra user confirmation. If you did, however, want to require a user to confirm settings (possibly while debugging your preseed file), you could comment out one of these options.

### Expert Partition Recipes

The predefined partition recipes that Ubuntu provides are probably adequate for basic servers, but most administrators I know have strong feelings about how their systems are partitioned. In these cases you will likely want to create your own custom partitioning scheme for your servers. In the preceding world this is known as an `expert_recipe`. Custom partitioning recipes can get rather complex as there are a lot of options available. The complete documentation is available at http://d-i.alioth.debian.org/svn/debian-installer/installer/doc/devel/partman-auto-recipe.txt, but even that can be difficult to follow without some examples.

First let’s examine a basic partitioning recipe that is provided in a lot of the example preseed files in official documentation. The following recipe will set up a small `/boot` partition and a swap partition and use up the rest of the disk for `/`:

```
d-i partman-auto/expert_recipe string                         \\
  boot-root ::                                               \\
    40 50 100 ext3                                           \\
            $primary{ } $bootable{ }                         \\
            method{ format }                                 \\
            use_filesystem{ } filesystem{ ext3 }             \\
            mountpoint{ /boot }                               \\
    .                                                         \\
```

