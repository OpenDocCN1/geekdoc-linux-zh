If we append this to the end of the */etc/lilo.conf* file, however, vmlinuz-2.3.12 won't become the default kernel that gets booted. In order for this to happen, we must do one of two things: Either we make this block the first block, or we use the *default* command. For our example, we'll use the *default* command. Because this command cannot be part of a block, we insert it at the beginning of the file, as shown here:

```
default=vmlinuz-2.3.12
```

And that's it. Here's the final */etc/lilo.conf* file:

```
default=vmlinuz-2.3.12
boot=/dev/hda
prompt
timeout=50
image=/boot/vmlinuz-2.2.5-15
label=linux
root=/dev/hda2
read-only
other = /dev/hda1
label = dos
table = /dev/hda
image=/boot/vmlinuz-2.3.12
label=linux-2.3.12
root=/dev/hda2
read-only
```

Now that the */etc/lilo.conf* file is edited and saved, all you need to do is run LILO.

# ## RUNNING LILO

Now that you are familiar with your */etc/lilo.conf* file, it's time to actually run the LILO boot manager program and let it do its important work. Usually this is a relatively un-eventful process.

In most cases, you will simply need to run LILO without any parameters. The result will look something like this:

```
[root@ford /boot]# li1o
Added linux
Added dos
```

LILO has taken the information from */etc/lilo.conf* and written it into the appropriate boot sector.