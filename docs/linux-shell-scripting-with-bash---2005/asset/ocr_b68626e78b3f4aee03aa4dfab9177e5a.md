+   • -info-script F (or -new-volume-script F or -F F)—For multi-volume archives, runs the given script at end of each volume

+   • -ignore-failed-read—Doesn't stop processing when a file cannot be read

+   • -ignore-zeros (-z)—Ignores blocks of zeros in the archive

+   • -incremental (-G)—Creates/lists/extracts using old GNU-format incremental backup

+   • -interactive (or -confirmation or -w)—User confirmation

+   • -keep-old-files (-k)—Doesn't overwrite existing files

+   • -label N (-V N)—Specifies volume label N

+   • -list (or -t)—Lists the files in the archive

+   • -listed-incremental (-g)—Creates/lists/extracts using new GNU-format incremental backup

+   • -modification-time (-m)—Doesn't change modification time on extracted files

+   • -multi-volume (-n)—Creates/lists/extracts multi-volume archive

+   • -null—With -files-from, tar expects names ending with ASCII NUL characters (that is, C strings)

+   • -old-archive (or -portability or -o)—Writes a Unix V7 format archive

+   • -one-file-system (-1)—Stays in the current file system when creating an archive

+   • -preserve—Same as -save-permissions and -same-order

+   • -read-full-blocks (-B)—R-eblocks as you read (for reading 4.2BSD pipes)

+   • -record-number (-R)—Shows record number within archive with each message

+   • -remove-files—Removes files added to the archive

+   • -to-stdout (-c)—Prints extracted files to standard output

+   • -same-permissions (or -preserve-permissions or -p)—Extracts all file permissions

+   • -starting-file F (-K F)—Begins extracting/listing at file F in the archive

+   • -same-order (or -preserve-order or -s)—Sorts extraction names to match the archive

+   • -same-owner—Makes extracted files have the same owner as the owner who added them

+   • -sparse (-S)—Handles sparse files efficiently

+   • -tape-length N (-L)—Changes volumes after writing N*1024 bytes

+   • -totals—Prints total bytes saved with -create

+   • -update (or -u)—Adds files if they are newer than the files already in the archive

+   • -verify (-v)—Verifies each archive after writing it