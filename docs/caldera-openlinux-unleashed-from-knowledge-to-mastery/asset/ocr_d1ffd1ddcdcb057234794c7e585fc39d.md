original kernel around in case the new one will not boot. Copy the kernel to a new file such as /boot/vmlinuz-2.2.5-rebuilt.

Next, you have to install a boot loader that can load the new kernel. Edit the file /etc/lilo.conf to do this. The simplest method is to copy the entry for the existing kernel and give it a new label. For example, the lilo entry for the old kernel might look something like this:

```
image = /boot/vmlinuz-2.2.5-modular
label = linux
root = /dev/hda1
vga = 274
read-only
append = 'debug=2'
```

Copy the entry so you end up with two entries like this:

```
#
# default entry
#
image = /boot/vmlinuz-2.2.5-rebuilt
label = linux
root = /dev/hda1
vga = 274
read-only
append = 'debug=2'
```

```
#
# additional entries
#
image = /boot/vmlinuz-2.2.5-modular
label = Original
root = /dev/hda1
vga = 274
read-only
append = 'debug=2'
```

# **Note**

The root and vga entries are examples from my system. You should use whatever values the Caldera OpenLinux installation procedure put in your /etc/lilo.conf file.