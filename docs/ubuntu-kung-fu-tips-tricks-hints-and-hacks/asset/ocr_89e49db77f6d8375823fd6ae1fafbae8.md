data. To use it, just type shred -u filename, replacing filename with the name of the file.

# Decrypting a file or folder

To decrypt a .pgp file, simply double-click it. You'll be prompted to type the passphrase you created during key production, so do so. You should now find the original file (or archive) is visible alongside the .pgp file.

Remember that it is only possible to decrypt a file on a computer on which the relevant encryption keys are installed. Usually this is the computer on which the keys were generated, unless the keys have been exported, as described in the following section.

# Exporting a key pair for use on another PC

It's a wise idea to backup your encryption keys because, without them, there is quite simply no way of decrypting files you've encrypted.

Alternatively, you might choose to install the same keys on two or more computers, so each is able to share encrypted files.

To do this, you need to export the key pair as a file.

If choose to do this, ensure you keep the key pair file safe because—perhaps obviously—anybody with the key file and your encrypted files will potentially be able to unlock them.

To export the key, first ensure the computer's time and date is correct (to learn how, see page 47). Then start the Password and Encryption Keys program. It can be found on the Applications ▸ Accessories menu. Ensure the My Personal Keys tab is selected and right-click your key in the list. Click Properties in the menu that appears, and click the Details tab in the dialog box. Finally, click the EXPORT button at the bottom right, and choose a location to save the key file.

To import a key in a different Ubuntu installation, first ensure the time and date is correct on the computer. Then start the Password and Encryption Keys program, as described above, and click Key ▸ Import on the menu. Finally, navigate to your saved key.

# Enhancing web browser security

Ubuntu 8.04 and 8.10 use version 3 of the Firefox browser. This has significant security features, such as protection against phishing, wherein users are redirected to fake websites in order to steal login