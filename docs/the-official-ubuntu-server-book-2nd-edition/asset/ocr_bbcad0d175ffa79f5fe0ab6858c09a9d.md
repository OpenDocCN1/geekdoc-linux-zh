options you would use for a DHCP install with the static settings, except comment out or remove the disable_dhcp option. Finally, add the following options to the preseed:

```
d-i netcfg/dhcp_failed note
d-i netcfg/dhcp_options select Configure network manually
```

With these options in place, on networks where DHCP works, the install will use those settings. In case DHCP fails, the installer will then fall back to your static settings.

# Partitioning

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

+   - **partman-auto/method**
+     This option defines what partitioning method to use for the automatic partitioning and can accept the options regular, lvm, or crypto. As the options suggest, the latter two set up partitions as LVM or encrypted volumes.

+   - **partman-auto/purge_lvm_from_device and partman-lvm/confirm**
+     These options just save you from having to acknowledge warning prompts in the installer. The former option will purge any old LVM