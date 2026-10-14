
to manually unlock the filestore! Alternatively, you can simply hit Enter to have a passphrase generated automatically, but you should print out the passphrase and store it in a secure location.

Once the commands have completed, log out and back in again.

When the desktop appears, you’ll find you have a new `/private` folder within your `/home` folder. As mentioned, this can be used just like a standard folder—files and folders can be stored there, and you will see no sign that the contents of the folder are in fact encrypted.

> **NOTE**  The third-party TrueCrypt software (www.truecrypt.org) allows you to create encrypted files on any version of Ubuntu, not just 8.10. My book *Ubuntu Kung Fu* explains how to use TrueCrypt and I’ve reproduced the TrueCrypt section on the book’s website: www.ubuntukungfu.org/truecrypt.html.

## Encrypting individual files and folders

Users of both Ubuntu 8.04 and 8.10 can encrypt individual files and folders. This is unrelated to encryption of the `/private` folder.

Here’s how this feature is typically used. Usually, a user encrypts a file, creating an encrypted copy. She then permanently deletes the original. If the user wishes to access the file again, she must decrypt the file. If the file is subsequently changed by editing, it must be re-encrypted afresh.

As you might guess, this type of encryption is best for files that you won’t access frequently, such as old files you wish to archive.

It makes use of public/private key cryptography. This is primarily used to encrypt email, but it can also be used to encrypt files.

> **NOTE**  The way key pair encryption works means encryption/decryption is limited to computers on which the key pair is installed. So, this isn’t an ideal way of creating encrypted files you wish to share with others.

## Creating a key pair

To encrypt and decrypt files, first you’ll need to create a key pair, as follows (this is a task you only need to do once):

1. Click the Password and Encryption Keys program. It’s on the Applications ⇨ Accessories menu.
2. Click the NEW button at the bottom of the program window. In the dialog box that appears, select PGP Key, and click CONTINUE.
3. Enter personal details, as requested. These details are relevant only if you intend to use the key pair to encrypt emails. If creating keys simply for personal encryption purposes, any details can be filled in, although note that you need to type a first and last name in the Full Name field. When done, click the CREATE button.
4. Enter a passphrase. This is what you'll need to type to decrypt any files you encrypt, so it's important you choose something memorable. It should also be as long as possible, and hard to guess. Spaces and symbols can be used. Enter the passphrase twice to confirm correct typing—once in the Password text field, and once in the Confirm field. Click OK when done.

> NOTE Do not forget the passphrase! If it is lost, any data you have encrypted is also lost. There is no way of recovering the data, and no way of cracking the encryption. Ubuntu uses 2,048-bit encryption keys. It is theorized that to crack such a key would take more time than the universe has been in existence!

5. Following this, the keys are created. This can take some time, depending on your PC's speed. Once it's finished, click to close the Passwords and Encryption Keys program window.

## Encrypting a file or folder

To encrypt a file or folder, simply right-click it and select Encrypt from the menu that appears. In the dialog box put a check alongside the key you created (there will probably only be one option), and click OK.

If encrypting a folder, you'll be asked if you want to encrypt each file in the folder separately, or package them all together in an archive. The latter is the best option, and you'll be asked to choose the archive type you want to use (i.e. .zip, .tar.gz etc.). The choice of compression format makes no difference to the encryption.

Once done, you'll find a new file alongside the original file or folder, with the same filename, but with an additional .pgp file extension. This is the encrypted version of the file or folder. If you chose to encrypt a folder and create an archive, the archive file will also be present.

The original file (and archive, if applicable) should be deleted.

> TIP To permanently delete a file or folder, rather than send it to the trash where it might be recovered, click it once and type Shift+Delete. Alternatively, delete it at the command-line. For extra security, use the shred command. This not only deletes files, but also destroys any "residue" left on the disk by overwriting the
