PuTTY session. Select *Add Key* to bring up a standard Window file browser. Find your private key and select it. Pageant will display a dialog box to request your passphrase. Enter it. If you can’t type your passphrase correctly, Pageant will ask you to do it again.

Once Pageant is ready, open a PuTTY session. Connect to a machine that has your public key installed. You should get a command prompt without needing to enter your passphrase.

If key-based authentication works when you specify a private key file, but not when using Pageant, verify that PuTTY is configured to use Pageant. Select *Connection->SSH->Auth*. Under *Authentication Methods*, you’ll find an *Attempt authentication using Pageant* checkbox. Make sure it’s checked.

Once you know that Pageant works, it’s helpful to have it start at login. Find your account’s Startup folder (the exact location varies depending on your version of Windows). In another window, find your Pageant program. It will probably be in the PuTTY directory under either *Programs* or *Program Files (x86)*. Create a link to Pageant in the startup directory.

For optimal convenience, have the shortcut load your private key at login. You can either give Pageant the full path to your key as an argument, or you can set a *Start in* directory and only use the short file name. I recommend setting the *Start in* directory, because it makes loading multiple keys at login much simpler. Right-click on your Pageant shortcut. Under *Target*, add the name of your private key file as an argument. The Target should now look something like `C:\Program Files\PuTTY\pageant.exe` moose.ppk. On that same screen, you’ll see a *Start in* field. Enter the full path to your keys directory there. On my laptop, that would be `c:\Users\mwlucas\Documents\keys`.

To verify this works, exit your running Pageant and double-click on the new icon in the startup folder. You should be prompted to enter the passphrase for your key. If it doesn’t work, you’ve probably messed up a path in the shortcut. Remember that you need to put quotes around any path with a space in it.

# Backing Up Key Files

If you lose your private key, your key pair is useless. Once you know your key pair works for authentication, back up both the private and public keys. The PuTTY .ppk file contains both the public and private keys, but OpenSSH key pairs need both files. Don’t just copy your private key to another machine—every machine that has your private key is another place your key can be stolen from. Back up your private key on off-line media, such as a flash drive or a CD. You might also encrypt it with a program like GnuPG. (If you are not familiar with GnuPG, I recommend the book *PGP & GPG: Email for the Practical*