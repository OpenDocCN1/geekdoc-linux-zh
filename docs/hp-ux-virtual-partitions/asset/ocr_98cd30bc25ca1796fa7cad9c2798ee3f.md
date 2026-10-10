One or more options other than -S, -a, -m, -d is specified more than once.

For the -a or -m option, an unavailable resource (allocated to another virtual partition or exceeding the available resource limit) is specified.

For the -m or -d option, the specified resource is not presently assigned to vp_name.

The state of the modified vPar following an error depends on the following factors:

+   *   If the error is detected during syntax and semantic checks of the command line, the vPar is not changed.

+   *   If the error is detected while actually modifying the vPar, AND you
+       are modifying an alternate database, the vPar is not
+       changed. This
+       is because changes are not committed until the end of the
+       command.

+   *   If the error is detected while modifying the vPar, AND
+       you are
+       modifying the database currently loaded into the monitor,
+       then any
+       changes made to the point of the error (working left-to-
+       right on
+       the command line) will remain. This is because changes to
+       the live
+       database are made incrementally, as they are requested.

# AUTHOR

vparmodify was developed by the Hewlett-Packard Company.

# SEE ALSO

vparboot(1M), vparcreate(1M), vparremove(1M), vparreset(1M), vparstatus(1M), vparresource(5), vpartition(5).