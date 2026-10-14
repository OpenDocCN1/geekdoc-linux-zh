5. Right-click the md5sum link corresponding to your selection. After it has downloaded both the extension and the corresponding md5.txt to the same directory, you must manually verify that you indeed have a valid download. To do this, use the command

```
$ md5sum -c extension_name.ext.md5.txt
```

The extension_name.ext is replaced by the name of the extension you downloaded. You should see OK as the result. If not, you must redownload until the extension can be validated by its checksums.

All of these extra and manual steps can be avoided by using our automated GUI download system.

# SAVING YOUR EXTENSIONS

Because DSL was created as a nomadic guest operating system, no drives or devices are automatically mounted. In fact, the default user dsl does not have administrator privileges to have write access to physical devices. The default for using the MyDSL system is to download the extensions to /tmp, which resides on the RAM disk (/ramdisk).

After downloading and trying the extension, you most likely want to keep it. Recall that MyDSL extensions were built with the live CD user in mind. Therefore, upon a reboot or shutdown, the extensions are gone.

Having a persistent store for your favorite extensions means you must mount a drive and copy the extensions to that location. There are many ways to accomplish this task:

+   File manager—Using one of the file managers to save files is discussed in Chapter 3, "Using DSL Applications." For this task, you have to select the root version of the appropriate file manager.

+   Save during shutdown—I did provide a sort of safety net upon shutdown. If you have any extensions still residing on the RAM disk-based /tmp directory, a dialog prompts you to save them. If you select OK, the system file manager emelfm opens with root privileges to allow you to save your extensions.

Remember that you can use the mounting tool in the lower-right corner of the DSL desktop to mount the partition from your hard disk or pen drive where you want to install the extension.