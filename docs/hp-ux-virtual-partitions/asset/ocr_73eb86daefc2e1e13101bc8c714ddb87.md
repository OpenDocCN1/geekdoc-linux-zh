support for a *graph* file which specifies files to be included and excluded, and other advanced features. **fbbackup** is an HP-UX-only utility, and tapes can be read using **frecover** on HP-UX systems only.

# dd

This is a bit-for-bit copy. It is not smart in the sense that it does not copy files and ownerships; it just copies bits. You could not, therefore, select an individual file from a **dd** tape as you could with **frecover**, **tar**, **restore** or **cpio**. **dd** is mainly used for converting data such as EBCDIC to ASCII.

# dump

**dump** is similar to **fbbackup**. If you use **fbbackup** on HP-UX, you will see much similarity when you use **dump**. **dump** provides the same-level backup scheme as **fbbackup** and creates /var/admin/dumpdates, which lists the last time a file system was backed up. **restore** is used to read information backed up with **dump**. **dump**, however, works only with HFS file systems and not VxFS, and it assumes that you are using a reel tape.