deledit Equivalent to delget, except that the get phase includes the -e option.

diffs Gives a diff listing between the current version of the files being edited and the versions in SCCS format. The [-rcixt] options are passed to get. The [-I-sefhb] options are passed to diff. The -C option is passed to diff as -c.

edit Equivalent to get -e.

enter Equivalent to create, except get is omitted. This pseedo command is useful when you want to run the edit command immediately after creating the SCCS file.

fix Removes a named delta, but leaves a copy of the delta in the current directory. The -r SID option is required and must point to a leaf in the source tree. Since a record of the changes is not preserved, fix should be used carefully.

info Lists all the files being edited. The -b option ignores branches in determining which files are being edited. The -u user option lists only the files being edited by user. The -U option is equivalent to -u current_user.

print Prints information about named files. Equivalent to prs -a followed by get -p -m -s.

tell Lists all the files being edited, with a newline after each entry. See the info section for a description of the -b, -u user and -U options.

unedit Equivalent to unget. Any changes made since the last get are lost. Use with caution.

Certain commands, admin, cdc, check, clean, diffs, info, rmdel, sccsdiff, and tell cannot use the set-user-id feature, as this would allow anyone to change the authorizations. These commands are always run as the real user.

Options
The options supplied to the SCCS commands are documented in the corresponding SCCS man pages. The options supplied to the pseudo commands are documented in the above section. All other options preceding command are documented as follows:

+   -r Runs sccs as the real user rather than the effective user sccs is set-user-id to.

+   -d rootpath Gives the pathname to be used as the root directory for the SCCS files. rootpath defaults to the current directory. This flag takes precedence over the PROJECTDIR environment variable.

+   -p dirpath Specifies the pathname for the SCCS files. The default is the SCCS directory. dirpath is appended to rootpath and is inserted before the final component of the pathname.

The command sccs -d/usr-p cmd get src/b converts to get /usr/src/cmd/s.b. This can be used to create aliases. For example,