Now that our final toolchain is in place, it is important to ensure that compiling and linking will work as expected.
We do this by performing the same sanity checks as we did earlier in the chapter:

```
echo 'int main()' > dummy.c
cc dummy.c -v -Wl,--verbose & dummy.log
readelf -l a.out | grep ': /lib'
```

There be no errors, and the output of the last command will be (allowing for platform-specific differences in dynamic linker):

[Requesting program interpreter: /lib64/ld-linux-x86-64.so.2]

Now make sure that we're set up to use the correct starts:

```
grep -o '/usr/lib.*crt[1]. *succeeded' dummy.log
```

The output of the last command should be:

```
/usr/lib/gcc/x86_64-pc-linux-gnu/9.2.0/.../lib/crt1 succeeded
/usr/lib/gcc/x86_64-pc-linux-gnu/9.2.0/.../lib/crti succeeded
/usr/lib/gcc/x86_64-pc-linux-gnu/9.2.0/.../lib/crt0 succeeded
```

Depending on your architecture, the may may differ slightly, the difference usually being the name of the directory after /usr/lib/gcc. The important thing to look for is that gcc has all three crt*.o files under /usr/lib directory.

Verify that the compiler is searching for the correct header files:

```
grep -B4 '^/usr/include' dummy.log
```

This command should return the following output:

```
#include <...> search starts here:
/usr/lib/gcc/x86_64-pc-linux-gnu/9.2.0/include
/usr/local/include
/usr/lib/gcc/x86_64-pc-linux-gnu/9.2.0/include-fixed
/usr/include
```

Again, note the directory named after your target triplet may be different than the above, depending on your architecture.

Next, verify if the linker is being used with the correct search paths:

```
grep 'SEARCH.*</usr/lib' dummy.log | sed 's| |\n|'
```

References to paths that components with '-linux-gnu' should be ignored, but otherwise the output of the last command should be:

```
SEARCH_DIR("/usr/x86_64-pc-linux-gnu/lib64")
SEARCH_DIR("/usr/local/lib64")
SEARCH_DIR("/usr/lib64")
SEARCH_DIR("/usr/x86_64-pc-linux-gnu/lib")
SEARCH_DIR("/usr/local/lib")
SEARCH_DIR("/usr/lib")
SEARCH_DIR("/usr/lib")
```