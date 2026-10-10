# ## BUGS

When piping an encrypted file into *more* and allowing *funzip* to prompt for password, the terminal may sometimes be reset to a non-echo mode. This is apparently due to a race condition between the two programs; *funzip* changes the terminal mode to non-echo before *more* reads its state, and *more* then “restores” the terminal to this mode before exiting. To recover, run *funzip* on the same file but redirect to /dev/null rather than piping into *more*; after prompting again for the password, *funzip* will reset the terminal properly.

There is presently no way to extract any member but the first from a ZIP archive. This would be useful in the case where a ZIP archive is included within another archive. In the case where the first member is a directory, *funzip* simply creates the directory and exits.

The functionality of *funzip* should be incorporated into *unzip* itself (future release).