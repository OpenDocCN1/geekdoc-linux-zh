# Configuring LILO

You configure LILO using the `/etc/lilo.conf` file. This file is generally broken into two main sections: global and per-image options. (The latter are kept in sections known as *stanzas*.) Some per-image options are further separated depending on whether they’re for a Linux kernel or another OS. To further confound the matter, many of the per-image options may be used at the global level to indicate a default value.

# Essential LILO Global Options

Listing 5.1 shows a typical `/etc/lilo.conf` file, including both global options and three stanzas for booting two Linux kernels and a non-Linux OS. Most configuration lines take the form `option=value`, but lines that begin with hash marks (#) are comments and are ignored. All but the first line of each stanza are traditionally indented. This practice makes it easy to spot where a new stanza begins.

# Listing 5.1: A Typical LILO Configuration File

```
# lilo.conf
# 
# Global Options:
# 
boot=/dev/hda
prompt
timeout=150
default=fedora
lba32
vga=normal
root=/dev/hda5
read-only
# 
# Kernel Options (may have multiple):
# 
image=/boot/vmlinuz-2.6.25
label=fedora
    initrd=/boot/initrd-2.6.25
    append="mem=2048M"
image=/boot/bzImage-2.6.26-experimental
label=debian
    root=/dev/hda6
# 
# Other Operating Systems Options (may have multiple):
# 
other=/dev/hda2
label=dos
```