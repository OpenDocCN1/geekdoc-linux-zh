
# Exercise 18-3: Configuring Public Key Authentication

**VIDEO** For more information, watch Exercise 18-3.

In this exercise, you will generate an RSA key pair on your client system and copy the public key to the SSH server to enable public key authentication. Complete the following:

1. Generate an RSA key pair on your client system by doing the following:
    - a. Log in to your client system as a standard user.
    - b. Open a terminal session.
    - c. At the shell prompt, enter `ssh-keygen -t rsa`.
    - d. When prompted for the file in which the private key will be saved, press **ENTER** to use the default filename of `~/ssh/id_rsa`.
    - e. When prompted, enter a passphrase for the key.

2. Configure the server system to use public key authentication by doing the following:
    - a. Copy the public key you just created to your SSH server system by entering `scp ~/ssh/id_rsa.pub user_name@address_of_SSH_server:mykeyfile`.
    - b. Enter the remote user’s password when prompted.
    - c. Establish an SSH session with the remote system as the user you intend to authenticate as using public key authentication. Use the following command: `ssh -l user_name address_of_SSH_server`.
    - d. Enter the remote user’s password when prompted.
    - e. At the shell prompt of the remote system, check to see if the `.ssh` hidden directory already exists by entering `ls -la` at the shell prompt. If the `.ssh` directory doesn’t exist, create it using the `mkdir ~/.ssh` command. Otherwise, go on to the next step.
    - f. At the shell prompt of the remote system, enter `cat mykeyfile >> ~/.ssh/authorized_keys`.
    - g. Enter `exit` at the shell prompt to close the SSH session.

3. Test the new configuration by doing the following:
    - a. At the shell prompt of your client system, enter `ssh -l user_name address_of_SSH_server`.
    - b. When prompted, enter the passphrase you assigned to your RSA private key. At this point, you should be automatically authenticated to the SSH server.
    - c. Close the session by entering `exit` at the shell prompt.

4. Configure ssh-agent to remember your private key passphrase by doing the following:
    - a. At the shell prompt of your client system, enter `ssh-agent bash`.
    - b. At the shell prompt, enter `ssh-add ~/.ssh/id_rsa`.
    - c. When prompted, enter the key file's passphrase. When you do, you should be prompted that the identity has been added.
    - d. At the shell prompt of your client system, enter `ssh -l user_name address_of_SSH_server`. You should be automatically authenticated to the SSH server without being prompted for the private key passphrase.

Great work! You're an SSH pro now! Before we end this chapter, there's one more encryption-related topic we need to address: encrypting files. Let's do that next.

## Encrypting Linux Files

Just as you can encrypt network transmissions between Linux systems using OpenSSH, you can also use encryption to protect files in the Linux file system. There are a wide variety of tools you can use to do this. Some are open source; others are proprietary. For your Linux+/LPIC-1 exam, you need to know how to use the open source GNU Privacy Guard (GPG) utility to encrypt files. Therefore, that's the tool we will use here. We'll discuss the following:

- How GPG works
- Using GPG to encrypt files

Let's begin by discussing how GPG works.

### How GPG Works

Gnu Privacy Guard (GPG) is an open source implementation of the OpenPGP standard (RFC 4880). It allows you to encrypt and digitally sign your data and communications. For example, you can encrypt files in your Linux file system. You can also encrypt and digitally sign e-mail messages.

GPG provides a cryptographic engine that can be used directly from the shell prompt using the `gpg` command-line utility. It can also be called from within shell scripts or other programs running on the system. For example, GPG support has been integrated into several popular Linux e-mail clients such as Evolution and KMail. It has also been integrated into instant messaging applications such as Psi.

A variety of graphical front ends are available for GPG as well. Some of the more popular front ends include KGPG and Seahorse. However, for your Linux+/LPIC-1 exam, you need to know how to use GPG from the shell prompt, so that's what we'll focus on in this chapter.

The recipient’s public key and sent along with the message that was encrypted using the symmetric key. When the recipient receives a message, GPG first decrypts the symmetric key using the user’s private key. GPG then uses the decrypted symmetric key to decrypt the rest of the message.

GPG supports many encryption algorithms, including the following:

- Symmetric encryption:
    - AES
    - 3DES
    - Blowfish
- Asymmetric encryption:
    - Elgamal
    - RSA
- Hashes:
    - MD5
    - SHA-1 and SHA-2
    - RIPEMD-160
- Digital signatures:
    - DSA
    - RSA

Now that you understand how GPG works, let’s review how you can use GPG to encrypt files.

### Using GPG to Encrypt Files

To encrypt a file using GPG, do the following:

1. Use GPG to generate your keys. To do this, enter `gpg --gen-key` at the shell prompt. An example is shown here:

    ```text
    rtracey@WS3:~-> gpg --gen-key
    gpg (GnuPG) 1.4.2; Copyright (C) 2005 Free Software Foundation, Inc.
    This program comes with ABSOLUTELY NO WARRANTY.
    This is free software, and you are welcome to redistribute it
    under certain conditions. See the file COPYING for details.

    gpg: directory '/home/rtracey/.gnupg' created
    gpg: new configuration file '/home/rtracey/.gnupg/gpg.conf' created
    gpg: WARNING: options in '/home/rtracey/.gnupg/gpg.conf' are not yet
    active during this run
    gpg: keyring '/home/rtracey/.gnupg/secring.gpg' created
    gpg: keyring '/home/rtracey/.gnupg/pubring.gpg' created
    Please select what kind of key you want:
       (1) DSA and Elgamal (default)
       (2) DSA (sign only)
       (5) RSA (sign only)
    Your selection?
    ```

2. Select the type of key you want to create. Usually you will use the default option (1), which uses DSA and Elgamal. You are prompted to specify the size of the key, as shown here:
    DSA keypair will have 1024 bits.
    ELG-E keys may be between 2024 and 4096 bits long.
    What keysize do you want? (2048)

3. Specify the size of key you want to create. Using the default size of 2048 bits is usually sufficient. You are prompted to configure the key lifetime, as shown here:
    Please specify how long the key should be valid.
    0 = key does not expire
    <n> = key expires in n days
    <n>w = key expires in n weeks
    <n>m = key expires in n months
    <n>y = key expires in n years
    Key is valid for? (0)

4. Specify when the key will expire. As shown in Step 3, you can specify that the key expire in a specified number of days, weeks, months, or years.

5. Next, construct your user ID for the key. The first parameter you need to specify is your real name. The name you specify is very important, as it will be used later during the encryption process. In the next example, I entered “rtracy” for my real name:
    You need a user ID to identify your key; the software constructs the user ID from the Real Name, Comment and Email Address in this form:
    "Heinrich Heine (Der Dichter) <heinrichh@duesseldorf.de>"
    Real name: rtracy

6. When prompted, enter your e-mail address.

7. When prompted, enter a comment of your choosing. You are prompted to confirm the user ID you have created for the key. An example is shown here:
    You selected this USER-ID:
    "rtracy (Hello World) <rtracy@sw3>"
    Change (N)ame, (C)omment, (E)mail or (O)Kay/(Q)uit?

8. If the information is correct, enter O to confirm the ID. You are prompted to enter a passphrase for the key, as shown here:
    You need a Passphrase to protect your secret key.
    Enter passphrase:

9. Enter a unique passphrase for the key. After doing so, you are prompted to perform various actions on the system while the key is generated. An example is shown here:
    We need to generate a lot of random bytes. It is a good idea to perform some other action (type on the keyboard, move the mouse, utilize the disks) during the prime generation; this gives the random number generator a better chance to gain enough entropy.
    +++,+++++ +++++ +++++ ++++++ +++++ +++++ +++++ ++++++++
