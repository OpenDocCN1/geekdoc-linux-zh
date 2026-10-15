FTS_DOT A file named "." or ".." which was not specified as a file name to fts_open() (see FTS_SEEDOT).

FTS_DP A directory being visited in post-order. The contents of the FTSENT structure will be unchanged from when it was returned in pre-order, i.e. with the fts_info field set to FTS_D.

FTS_ERR This is an error return, and the fts_errno field will be set to indicate what caused the error.

FTS_F A regular file.

FTS_NS A file for which no stat information was available. The contents of the fts_statp field are undefined. This is an error return, and the fts_errno field will be set to indicate what caused the error.

FTS_NSOK A file for which no stat information was requested. The contents of the fts_statp field are undefined.

FTS_SL A symbolic link.

FTS_SLNONE A symbolic link with a non-existent target. The contents of the fts_statp field reference the file characteristic information for the symbolic link itself.

Some immediate observations from the above information are that:

+   - The fts_info member has information similar to that found in the integer passed to the (*fn) function by nftw().
+   - Unlike the nftw() function, fts provides hooks for the application to use. In particular, fts_number and fts_pointer are two members of the returned structure that can be used for application specific data, making it possible to change state and data among different invocations of the fts_read() function.
+   - The fts_parent field provides a means to access the parent node, unlike nftw().
+   - It has stat information for the returned file in the fts_statp member, unless fts_info is either FTS_NS or FTS_NSOK.
+   - The name of the file is in the fts_name member. The fts_path member has the pathname of the file relative to the root of the search. For all practical purposes, this is the same path as fts_accpath.

It is also important to know that a single buffer is used for the various path members of all FSTENT structures of all files in file hierarchy. Because of this, there is no guarantee that the fts_path and fts_accpath members of a previously returned FTSENT structure are still properly null-terminated, because they might have been written over already. Only the fts_path and fts_accpath members of the file most recently returned by fts_read() are guaranteed to be null-terminated. To use these fields to reference any files represented by other FTSENT structures will require that the path buffer be modified using the information contained in that FTSENT structure's fts_pathlen field. Any such modifications should be undone before further calls to fts_read() are attempted. In contrast, the fts_name field is always null-terminated.