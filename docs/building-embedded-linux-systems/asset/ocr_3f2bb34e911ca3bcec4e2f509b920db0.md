```
> done
$ cp -d id*.so* $(PRJROOT)/rootfs/lib
```

The first cp command copies the actual shared libraries, the second one copies the major revision version symbolic links, and the third one copies the dynamic linker and its symbolic link. All three commands are based on the rules outlined earlier in this section regarding the naming conventions of the different files in $[TARGET_PREFIX]/lib. The -d option is used with the second and third cp commands to preserve the symbolic links as-is. Otherwise, the files that the symbolic links point to are copied in their entirety.

Of course, you can remove the libraries that are not used by your applications from the list in the set of commands shown. If you would rather have the complete set of libraries included in glibc on your root filesystem, use the following commands:

```
$ cd $[TARGET_PREFIX]/lib
$ cp *-*.so $(PRJROOT)/rootfs/lib
$ cp -d *.so.\[*-9] $(PRJROOT)/rootfs/lib
$ cp libSegFault.so libmwmusage.so libpcapprofile.so \
> $(PRJROOT)/rootfs/lib
```

If you have applications that use the glibc NSS, don't forget to copy the libnss_SERVICE libraries you need to your target's root filesystem. libnss_files and libnss_dns are the ones most often used. You will also need to copy the sample nsswitch.conf provided with glibc to your target's /etc directory and customize it to your setup:$1

```
$ cp $(PRJROOT)/build-tools/glibc-2.2.1/nss/nsswitch.conf \
> $(PRJROOT)/rootfs/etc
```

Whether you copy all or part of the glibc libraries, you will notice that some of these libraries are large. To reduce the size of the libraries installed, you can use the cross-platform strip utility you built in Chapter 4. Be careful not to strip the original libraries, because you would have to install them all over again. Strip the libraries only after you copy them to the root filesystem:

```
$ powerpc-linux-strip $(PRJROOT)/rootfs/lib/*.{so,}
```

On our control module, the $(PRJROOT)/rootfs/lib directory with all the glibc libraries weighs around 10 MB before stripping. Stripping all the libraries reduces the directory size to 2.5 MB.

The glibc components have now been installed on the target's root filesystem and are ready to be used at runtime by your applications.

> 1 Have a look at Linux Network Administrator's Guide by Tony Baus, Terry Dawson, and Gregor Purdy (O'Reilly) for details about the customization of the nsswitch.conf file.