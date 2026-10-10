.example.com. If you want to rename the file, you can do so by including the new name following the colon.

# ## Configuring Logins without Passwords

If you use SSH a lot, or if you use it in automated tools, you'll no doubt become annoyed by the need to type a password with every connection. There is a way around this requirement: You can set up the SSH client with keys and give the public key to the server computer. With this configuration, the SSH client computer can identify itself, possibly obviating the need for you to type a password.

> WARNING  Configuring SSH to operate without the use of passwords is convenient, but it does increase security risks. If somebody you don't trust ever gains access to your account on the SSH client system, that person will be able to log into the SSH server system as you without the benefit of your password. Thus, you should create a password-less login only from a client that's very well protected, if at all. Configuring access to the root account in this way is particularly risky.

To configure SSH to not require a password, follow these steps:

+   1. Log into the SSH client system as the user who will be performing remote access.
+   2. Type the following command to generate a version 2 SSH key: `\$ ssh-keygen -q -t rsa -f \`/.ssh/\`id_rsa -C `` `-N ``"`
+   3. Step 2 generates two files: id_rsa and id_rsa.pub. Transfer the second of these files to the SSH server computer in any way that's convenient—via floppy disk, by using scp, or by any other means. Copy the file under a temporary name, such as *temp.rsa*.
+   4. Log into the SSH server system. If you use SSH, you'll need to type your password.
+   5. Add the contents of the file you've just transferred to the end of the `\`/.ssh/authorized_keys` file. (This file is sometimes called `\`/.ssh/authorized_keys2`, so you should check to see which is present. If neither is present, you may need to experiment.) Typing `cat \`/temp.rsa >> \`/.ssh/authorized_keys` should do this job, if you stored the original file as `\`/temp.rsa`.

If you now log out of the SSH server system and try to log in again via SSH from the client, you shouldn't be prompted for a password; the two computers handle the authentication automatically. If this doesn't work, chances are the `\`/.ssh/authorized_keys` file needs another name, as described earlier. You may also want to check that the file includes a line matching the contents of the original public-key file on the client. Some older clients may require you to specify that you use version 2 of the SSH protocol by including the `-2` option:
`\$ ssh -2 server`