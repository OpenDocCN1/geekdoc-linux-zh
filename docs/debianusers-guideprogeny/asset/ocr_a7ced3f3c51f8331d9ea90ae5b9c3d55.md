+   ▾ The < pipe redirects the files described by the string to the target.
+   ▾ The target is the directory to which to restore files.

# The -i Flag for the cpio Command (Restore)

| Option | Action | Comments |
| :--- | :--- | :--- |
| ▾ -f<br>▾ --non-matching | Copies all files except those that match the string | |
| -m | Keeps previous modification time on restored files. | |
| ▾ -d<br>▾ --make-directories | Makes directories as needed. | |
| ▾ -u<br>▾ --unconditional | Over writes old files. | |
| ▾ -R USER GROUP<br>▾ --owner USER GROUP | Reassigns file ownership. | This option can only be used by the root user.<br><br>If no user is specified, the root user becomes the owner. |
| -r | Renames files. | Provide new file names when prompted. |