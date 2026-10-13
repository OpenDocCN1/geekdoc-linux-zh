Rock Ridge is an extension to ISO 9660 that provides all of these UNIX-like features. Basically there are extensions to each directory record that supply all the additional information, and when Rock Ridge is in use, the file system is indistinguishable from a normal UNIX file system (except that it is read-only, of course).

+   - —Disable the use of Rock Ridge extensions, even if available. (Compare to map.)
+   - `check=r[elaxed] / check=s[trict]`—With check=relaxed, a filename is first converted to lowercase before doing the lookup. This is probably only meaningful together with norock and map=normal. (Default: check=strict.)
+   - `uid=value and gid=value`—Give all files in the file system the indicated user or group id, possibly overriding the information found in the Rock Ridge extensions. (Default: uid=0,gid=0.)
+   - `map=n[ormal] / map=o[ff]`—For non-Rock Ridge volumes, normal name translation maps upper to lowercase ASCII, drops a trailing ;1, and converts ; to .. With map=off no name translation is done. See norock. (Default: map=normal.)
+   - `mode=value`—For non-Rock Ridge volumes, give all files the indicated mode. (Default: read permission for everybody.) Since Linux 2.1.37, one no longer needs to specify the mode in decimal. (Octal is indicated by a leading 0.)
+   - `unhide`—Also show hidden and associated files.
+   - `block=[512|1024|2048]`—Set the block size to the indicated value. (Default: block=1024.)
+   - `conv=a[uto] / conv=b[inary] / conv=m[text] / conv=t[ext]`—(Default: conv=binary.) Since Linux 1.3.54, this option has no effect anymore. (And non-binary settings used to be very dangerous, often leading to silent data corruption.)
+   - `cruft`—If the high byte of the file length contains other garbage, set this mount option to ignore the higher order bits of the file length. This implies that a file cannot be larger than 16MB. The cruft option is set automatically if the entire CD-ROM has a weird size (negative, or more than 800MB). It is also set when volume sequence numbers other than 0 or 1 are seen.

# ## MOUNT OPTIONS FOR minix

None.

# ## MOUNT OPTIONS FOR msdos

See mount options for fat. If the msdos file system detects an inconsistency, it reports an error and sets the file system read-only. The file system can be made writeable again by remounting it.