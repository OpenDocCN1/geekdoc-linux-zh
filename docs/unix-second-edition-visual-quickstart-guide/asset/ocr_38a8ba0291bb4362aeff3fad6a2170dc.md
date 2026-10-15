# To find and act on files:

+   find ~/ -name "*.backup" -ok rm {} \;

Type find with a wildcard expression, followed by -ok (to execute the following command, with confirmation), rm (the command to issue), and {} \; to fill in each file found as an argument for the command. If you want to, say, compress matching files without confirmation, you might use find ~/ -name "*.backup" -exec compress {} \; to do the work for you.

# Tips

+   On some Unix systems, you may not need the -print flag. Try entering find without the -print flag. If you see the results onscreen, then you don't need to add the -print flag.

+   Avoid starting the find command with the root directory, as in find / -name the_missing_file -print. In starting with the root directory (indicated by the /), you'll likely encounter a pesky error message for each directory you don't have access to, and there will be a lot of those. Of course, if you're logged in as root, this doesn't apply.

+   If you know only part of the filename, you can use quoted wildcards with find, as in find . -name 'info*' -print.

+   find offers many chapters worth of options. If you're looking for a specific file or files based on any characteristics, you can find them with find. For example, you can use find /home/shared -mtime -3 to find all files under the shared directory that were modified within the last three days. See Appendix C for a substantial (but not comprehensive) listing of options.