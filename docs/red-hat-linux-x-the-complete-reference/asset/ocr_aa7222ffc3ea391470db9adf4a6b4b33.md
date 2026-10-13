```
make install
```

If you want, you could enter these all on fewer lines, separating the commands with semicolons, as shown here:

```
make dep; make clean; make bzImage; make modules
```

```
make modules_install; make install
```

A safer way to perform these operations on single lines is to make them conditionally dependent on one another, using the && command. In the preceding method, if one operation has an error, the next one will still be executed. By making the operations conditional, the next operation is run only if the preceding one is successful.

```
make dep && make clean && make bzImage
```

```
make modules
```

```
make modules_install && make install
```

# Installing the Kernel Image Manually

To install a kernel bzImage file manually, copy the bzImage file to the directory where the kernel resides and give it the name used on your distribution, such as vmlinuz-2.4.22-1. Remember to first back up the old kernel file, as noted in the precautionary steps. vmlinuz is a symbolic link to an actual kernel file that will have the term vmlinuz with the version name. So, to manually install a bzImage file, you copy it to the /boot directory with the name vmlinuz and the attached version number such as vmlinuz-2.4.22-1. You then create a symbolic link from /boot/vmlinuz to /boot/vmlinuz-2.4.22-1.

```
make bzImage
```

```
cp arch/i386/boot/bzImage /boot/vmlinuz-2.4.22-1
```

```
ln -s /boot/vmlinuz /boot/vmlinuz-2.4.22-1
```