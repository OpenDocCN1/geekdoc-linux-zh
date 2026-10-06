# ci

Creates or records changes in an RCS file

ci [options] | file-list

The ci (check in) utility creates or records changes in RCS-encoded files. It is part of RCS (Revision Control System—page 871), a group of related utilities that manages the storage, retrieval, and updating of source files. The RCS utilities covered in Part III are ci, co, rcs, and rlog.

# Arguments

The file-list is a list of filenames, typically working filenames. For each of the named files, ci creates or changes the corresponding RCS file in the subdirectory RCS of the working file's directory, if one exists, or in the working file's directory otherwise. See the following “Notes” for more about RCS and working.

# Options

+   -d[date] date Specifies the check-in date and time. Many different formats are accepted for date. Enclose date within quotation marks if it contains any blanks.

+   -k[revision-number] keyword Checks in revision with existing keyword values for author, date, and revision. This method preserves identifying information attached to source files obtained from other sites. This option is usually used for initial check only.

+   -l[revision-number] lock After checking in the revision, retrieves a locked (editable) copy at the next revision level. This is a one-step equivalent to running ci by -l.

+   -m[comments] messages Allows you to enter a reason for checking in a revision to the file. If you do not use the -m option and standard input is a terminal, ci prompts you for comments. To create a null comment, do not enter anything after the -m option or enter a period (.) in response to the prompt for comments.

+   -n[name] name Assigns the symbolic name to the revision. This option allows you to give meaningful names to revisions so that you can access them more easily.

+   -r[revision-number] revision Specifies the revision number for the RCS-encoded file that is being in. This option is needed only if you do not use the default revision-number.

+   -u[revision-number] unlock After checking in the revision, retrieves an unlocked (unwritable) copy at the current revision level. This is a one-step equivalent to running ci by -u.