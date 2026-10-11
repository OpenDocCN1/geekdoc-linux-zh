For systems where iconv() is not available or where iconv()’s locales are not compatible with Windows, UTF-8 is the only locale available.

There are no systems that use UTF-8 as the default locale for Japanese.

Some broken filenames may be displayed, and some commands that cannot handle non-ASCII filenames may be aborted during parsing filenames. Especially, there may be `\` (\(0xfc)) in filenames, which must be handled carefully, so you had better not touch filenames written from Windows on UNIX.

In addition, although it is not directly concerned with Samba, since there is a delicate difference between the iconv() function, which is generally used on UNIX, and the functions used on other platforms, such as Windows and Java, so far as concerns the conversion between Shift_JIS and Unicode UTF-8 must be done with care and recognition of the limitations involved in the process.

Although Mac OS X uses UTF-8 as its encoding method for filenames, it uses an extended UTF-8 specification that Samba cannot handle, so UTF-8 locale is not available for Mac OS X.

# **Shift_JIS series + vfs_cap (CAP encoding)**

CAP encoding means a specification used in CAP and NetAtalk, file server software for Macintosh. In the case of CAP encoding, for example, if a Japanese filename consists of 0x8baa and 0x9f4c, and “txt” is written from Windows on Samba, the filename on UNIX becomes “:8baa:9f4c.txt” (a 14 bytes ASCII string).

For CAP encoding, a byte that cannot be expressed as an ASCII character (0x80 or above) is encoded in an “:xx” form. You need to take care of containing a `\` (\(0x5c)) in a filename, but filenames are not broken in a system that cannot handle non-ASCII filenames.

The greatest merit of CAP encoding is the compatibility of encoding filenames with CAP or NetAtalk. These are respectively the Columbia Appletalk Protocol, and the NetAtalk Open Source software project. Since those software applications write a file name on UNIX with CAP encoding, if a directory is shared with both Samba and NetAtalk, you need to use CAP encoding to avoid non-ASCII filenames from being broken.

However, recently, NetAtalk has been patched on some systems to write filenames with EUC-JP (e.g., Japanese original Vine Linux). In this case, you need to choose EUC-JP series instead of CAP encoding.

vfs_cap itself is available for non-Shift_JIS series locales for systems that cannot handle non-ASCII characters or systems that share files with NetAtalk.

To use CAP encoding on Samba-3, you should use the unix charset parameter and VFS as in Example 29.5.1.

You should set CNF42 if using GNU libiconv for unix charset. With this setting, filenames in the “cap-share” share are written with CAP encoding.