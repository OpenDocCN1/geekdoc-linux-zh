# Zipping Files and Directories with zip

If you're working with files and directories that will be accessed on the Windows platform, you might need to use zip (rather than gzip). This zip is like DOS or Windows zip, so it's a safer option than gzip, which can work, but it depends on the software available on the Windows system. zip files are compressed to save disk space and sometimes contain multiple files (see Code Listing 13.12).

# To zip files or directories with zip:

+   1. ls -l z*
+   
+   At the shell prompt, use ls -l to confirm the names of the files or directories you want to zip.
+   
+   2. zip -r zipped zipadeedoodah
+   
+   Type zip -r followed by the name of the zip file you're creating (without an extension), followed by the name of the file or directory to zip. Then just twiddle your thumbs while waiting for Unix to zip your files (Code Listing 13.12).

# Tips

+   - Some Unix systems don't offer the zip command. In this case, if you need to share files with Windows users, use either gzip or compress, send the file, and tell your colleagues that they can use WinZip, among other programs, to extract the files.
+   - If you zip a directory (remember to include the -r for recursive argument), you zip all the files within it.
+   - If you can't get the tune "Zip-A-Dee-Doo-Dah" out of your head after these examples, try humming "The Candy Man" or "I'd Like to Teach the World to Sing", or whistling the "Colonel Bogey March" (theme from The Bridge on the River Kwai).

```
[ejr@hobbes compression]$ ls -l z*
-rw-r--r-- 1 ejr users 501760 Jul 27 10:22 zipadeedoodah
[ejr@hobbes compression]$ zip -r zipped zipadeedoodah
adding: zipadeedoodah (deflated 52%)
[ejr@hobbes compression]$ ls -l z*
-rw-r--r-- 1 ejr users 501760 Jul 27 10:22 zipadeedoodah
-rw-r--r-- 1 ejr users 239943 Jul 27 10:41 zipped.zip
[ejr@hobbes compression]$
```

Code Listing 13.12 Use zip to compress files, particularly those you'll share with Windows users.