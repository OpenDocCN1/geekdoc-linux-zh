+   • A C object file (*file.o*).
+   • A **make** argument called a *make target*. This type of target enables you to type some of the standard installation instructions, such as **make install**, automating the entire process.
+   • The executable program itself.

The *requirements* refer to object files that have to be built before this particular target's instructions can be run. This is simply a space-separated list of object files. Finally, the *instructions* are typically simple *gcc* commands. A brief Makefile might be similar to the following:

```
```text
main : main.o sub1.o sub2.o
       gcc -o aill main.o sub1.o sub2.o
main.o : main.c
        gcc -c main.c
sub1.o : sub1.c
        gcc -c sub1.c
sub2.o : sub2.c
        gcc -c sub2.c
```
```

> **NOTE:** Manuals for all the GNU tools discussed here are available at [www.gnu.org/manual/manual.html](http://www.gnu.org/manual/manual.html).