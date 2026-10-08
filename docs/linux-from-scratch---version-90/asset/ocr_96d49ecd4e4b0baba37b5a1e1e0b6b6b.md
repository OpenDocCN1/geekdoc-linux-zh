# 6.10. Adjusting the Toolchain

Now that the final C libraries have been installed, it is time to adjust the toolchain so that it will link any newly compiled program against these.

First, backup the /tools linker, and replace it with the adjusted linker we made in chapter 5. We'll also create a link to its counterpart in /tools/$(uname -m)-pc-linux-gnu/bin:

```
mv -v /tools/bin/(ld,ld-old)
mv -v /tools/$(uname -m)-pc-linux-gnu/bin/(ld,ld-old)
mv -v /tools/bin/(ld-new,ld)
ln -sv /tools/bin/ld /tools/$(uname -m)-pc-linux-gnu/bin
```

Next, adjust the GCC specs file so it points to our new dynamic linker. Simply deleting all instances of "tools" leaves us with the correct path to the dynamic linker. Also adjust the spec file so that GCC knows where to find the correct headers and Glibc start. A sed command accomplishes this:

```
gcc -dumpspecs | sed -e 's@/tools@@g' \
-e '\*startfile_prefix_spec;/(n;s@*/usr/lib/@@' \
-e '\*cpp:n@ -system /usr/include/@@' \
-e '\*diname $(gcc --print-libgcc-file-name)\' /specs
```

It is a good idea to inspect the spec file to verify the intended change was actually made.
It is imperative to ensure that the basic functions (compiling and linking) of the adjusted toolchain are working as expected. To do this, perform the following sanity checks:

```
echo 'int main()' > dummy.c
cc dummy.c -v -Wl,--verbose &> dummy.log
readelf -l a out | grep ':lib'
```

There should be no errors

Note that on 64-bit systems /lib is the location of our dynamic linker, but is accessed via a symbolic link in /lib64.

> Note
On32-bit systems the interpreter should be /lib/ld-linux.so.2.

Now make sure you're set up the start scripts:
The output of the last command should be:

```
/usr/lib/../../crt1.o succeeded
/usr/lib/../../crt.o succeeded
/usr/lib/../../crtn.o succeeded
```