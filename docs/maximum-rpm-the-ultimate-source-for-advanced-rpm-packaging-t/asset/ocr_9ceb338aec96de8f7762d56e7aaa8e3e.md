The three checksums RPM uses to determine what should be done with a config file are

+   - The MD5 checksum of the file when it was originally installed. We'll call this the checksum of the original file.

+   - The MD5 checksum of the file as it exists at upgrade time. We'll call this the checksum of the current file.

+   - The MD5 checksum of the corresponding file in the new package. We'll call this the checksum of the new file.

Let's take a look at the various combinations of checksums, see what RPM will do because of them, and discuss why. In the following examples, we'll use the letters X, Y, and Z in place of lengthy MD5 checksums.

# 4.1.1.1. Original File = X, Current File = X, New File = X

In this case, the file originally installed was never modified. Or, as some sticklers for detail may note, it may have been modified, and subsequently those modifications were undone. The file in the new version of the package is identical to the file on disk.

In this case, RPM installs the new file, overwriting the original. You might be wondering why anyone would go to the trouble of installing the new file if it’s just the same as the existing one. The reason is that aspects of the file other than its name and contents might have changed. The file’s ownership, for example, might be different in the new version.

# 4.1.1.2. Original File = X, Current File = X, New File = Y

The original file has not been modified, but the file in the new package is different. Perhaps the difference represents a bug fix or a new feature. It makes no difference to RPM.

In this case, RPM installs the new file, overwriting the original. This makes sense. If it didn’t, RPM would never permit newer, modified versions of software to be installed! The original file is not saved because it had not been changed. A lack of changes here means that no site-specific modifications were made to the file.

# 4.1.1.3. Original File = X, Current File = Y, New File = X

Here we have a file that was changed at some point. However, the new file is identical to the existing file prior to the local modifications.

In this case, RPM takes the viewpoint that since the original file and the new file are identical, the modifications made to the original version must still be valid for the new version. It leaves the existing, modified file in place.