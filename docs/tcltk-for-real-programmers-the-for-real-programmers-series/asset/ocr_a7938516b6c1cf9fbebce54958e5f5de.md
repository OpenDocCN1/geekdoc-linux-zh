3. Compile the libraries and build the demonstration program "bltwish".
make

4. Test by running the demos.
Go into the demos directory:
cd demos
and run the test scripts.
./graph

If your system doesn't support "#!" in shell scripts, then run
../bltwish ./graph

5. Install BLT.
make install

The following directories will be created when BLT is installed. By default, the top directory is /usr/local/blt.

| bin | include | lib | man |
| blt2.4e | |
| demos | dd_protocols |

You can change the top directory by supplying the --prefix=dir switch to: ./configure.

Add the following lines to your program's Tcl_AppInit routine in tkAppInit.c

```
if (Blt_Init(interp) != TCL_OK) {
    return TCL_ERROR;
}
```