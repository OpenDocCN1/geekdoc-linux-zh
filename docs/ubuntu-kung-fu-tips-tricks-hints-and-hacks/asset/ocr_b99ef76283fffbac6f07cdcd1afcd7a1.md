It’s not a good idea to scan the entire filesystem using ClamTK, because ClamAV simply isn’t built for that task. In fact, in my tests, any attempt to do a full filesystem scan caused ClamAV/TK to crash.

Therefore, you should limit scans to your /home folder. This is where virus-infected files are most likely to be found because it’s where most files you download will end-up.

> NOTE If you’re worried about getting a virus when installing software, don’t be. All software in the Ubuntu repositories is digitally signed. This is a method of ensuring the files can’t be tampered with. It’s true that any software packages you manually download and install might contain viruses, but it’s very unlikely.

Before starting a scan, ensure that ClamAV scans hidden files by clicking Options ⇨ Scan Hidden Files (*).

To start a scan of your /home folder, click File ⇨ Home (Thorough). If using Ubuntu 8.04, click File ⇨ Full Home Scan.

Any virus-infected files found will be listed under the File heading in the ClamTK program window, along with their location (path). The type of virus infection will be listed under the Status heading.

You may see other files listed in the results area after a scan. If a file was too big to scan, it will be listed. If you wish to have ClamAV scan all files, regardless of size, click Options ⇨ No Maximum Size. Bear in mind this may dramatically increase the time taken to scan.

ClamAV is unable to remove any virus infections found in a file. Instead, the user must decide the course of action to take. Usually, deleting the file is best.

All antivirus programs are prone to false positives—identifying files as containing viruses when they don’t. To guard against this, should ClamAV report what it thinks is an infected file, search Google, specifying the name of the file and the name of the virus. If one or more people have encountered a similar result, that can help identify a false alarm.

# Encrypting files and folders

Encryption is a method of encoding files so that they can’t be accessed without first being decoded. This usually requires a passphrase.

The goal of encryption is usually to stop unauthorized individuals accessing private data. You might choose to encrypt personal files, for example, such as bank statements. Or you might choose to encrypt a file