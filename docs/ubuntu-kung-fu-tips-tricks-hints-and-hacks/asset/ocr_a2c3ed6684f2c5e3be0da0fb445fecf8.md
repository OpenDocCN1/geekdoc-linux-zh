to manually unlock the filestore! Alternatively, you can simply hit Enter to have a passphrase generated automatically, but you should print out the passphrase and store it in a secure location.

Once the commands have completed, log out and back in again.

When the desktop appears, you’ll find you have a new `/private` folder within your `/home` folder. As mentioned, this can be used just like a standard folder—files and folders can be stored there, and you will see no sign that the contents of the folder are in fact encrypted.

> **NOTE**  The third-party TrueCrypt software (www.truecrypt.org) allows you to create encrypted files on any version of Ubuntu, not just 8.10. My book *Ubuntu Kung Fu* explains how to use TrueCrypt and I’ve reproduced the TrueCrypt section on the book’s website: www.ubuntukungfu.org/truecrypt.html.

# Encrypting individual files and folders

Users of both Ubuntu 8.04 and 8.10 can encrypt individual files and folders. This is unrelated to encryption of the `/private` folder.

Here’s how this feature is typically used. Usually, a user encrypts a file, creating an encrypted copy. She then permanently deletes the original. If the user wishes to access the file again, she must decrypt the file. If the file is subsequently changed by editing, it must be re-encrypted afresh.

As you might guess, this type of encryption is best for files that you won’t access frequently, such as old files you wish to archive.

It makes use of public/private key cryptography. This is primarily used to encrypt email, but it can also be used to encrypt files.

> **NOTE**  The way key pair encryption works means encryption/decryption is limited to computers on which the key pair is installed. So, this isn’t an ideal way of creating encrypted files you wish to share with others.

# Creating a key pair

To encrypt and decrypt files, first you’ll need to create a key pair, as follows (this is a task you only need to do once):

+   1. Click the Password and Encryption Keys program. It’s on the Applications ⇨ Accessories menu.
+   
+   2. Click the NEW button at the bottom of the program window. In the dialog box that appears, select PGP Key, and click CONTINUE.