
Occasionally, if you download software outside of a package manager, you will need to manually install its runtime shared libraries. You can use `ldd` on a binary file to figure out its dependencies, then search for those dependencies within the package manager.

### Notes

You can use the `LD_LIBRARY_PATH` environment variable, instead of `ld.so.conf`, to enable additional library directories. However, in most situations, this is not recommended.
