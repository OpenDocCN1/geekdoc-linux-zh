
b. At the shell prompt, use the `ls` command to verify that the mytestfile.txt.gpg file was created.

4. Decrypt the file you just created by doing the following:

   a. Enter `gpg --output mytestfile.txt.decrypted --decrypt mytestfile.txt.gpg` at the shell prompt to decrypt the file.

   b. Use the `cat` command to display the contents of the mytestfile.txt.decrypted file and verify that it matches the content of the original file.

5. Send the encrypted file to a different system and decrypt it there by doing the following:

   a. If necessary, boot your second Linux system and log in as a standard user.

   b. Use the `ping` command to verify that it can communicate over the network with the first Linux system, where you exported the GPG public key.

   c. Switch back to your first Linux system.

   d. From the shell prompt of your first Linux system, export your public key by entering `gpg --export key_user_name > gpg.pub`.

   e. Use the `scp` command to copy the `gpg.pub` and `mytestfile.txt.gpg` files from your first Linux system to your second Linux system.

   f. Switch over to your second Linux system.

   g. Verify that the `gpg.pub` file was copied to your user’s home directory.

   h. Import the public key from your first Linux system into the GPG keyring by entering `gpg --import ~/gpg.pub` at the shell prompt.

   i. Verify that the public key was imported by entering `gpg --list-keys` at the shell prompt.

   j. Decrypt the encrypted file you copied over from the first Linux system by entering `gpg --output mytestfile.txt.decrypted --symmetric mytestfile.txt.gpg` at the shell prompt.

   k. When prompted, enter the passphrase you assigned to the GPG key when you created it on the first system.

   l. Use the `cat` command to display the contents of the mytestfile.txt.decrypted file and verify that it matches the content of the original file on the first Linux system.

You did it! You’re an SSH and GPG expert! Let’s review what you learned in this chapter.

## Chapter Review

In this chapter, you learned how to use encryption to secure data on a Linux system. We first looked at encrypting network communications with OpenSSH, and then we looked at using GPG to encrypt Linux files.

We began this chapter by reviewing how encryption works. The first type of encryption we looked at was symmetric encryption. With symmetric encryption, the key used to encrypt a message is the same key used to decrypt the message. That means the sender and the receiver must both have the exact same key. One of the key advantages of using symmetric encryption is speed. It processes much faster than asymmetric encryption. One of the difficulties associated with symmetric encryption is how to securely distribute the key to all the parties that need to communicate with each other. Examples of cryptographic standards that use symmetric encryption include:

- 3DES
- AES
- Blowfish

When selecting an encryption scheme, you should pick one that supports a minimum of 128 bits. The longer the key, the more secure the data is.

We then turned our attention to asymmetric encryption. Asymmetric encryption uses two keys instead of one: the public key and the private key. Data that has been encoded with the public key can be decoded only with the private key. Data that has been encoded with the private key can only be decoded with the public key. Asymmetric encryption is frequently referred to as public key cryptography. Commonly used asymmetric encryption mechanisms include:

- RSA
- DSA

Private/public key pairs should be much longer than those used for symmetric encryption. They should be 1024 bits or longer.

You will frequently see implementations that use a hybrid of both symmetric and asymmetric encryption. Symmetric encryption is used for an initial key exchange to securely copy a secret key to both parties in a session. Once done, both parties have the same key and can switch to symmetric encryption for the remainder of the session.

A certificate authority is responsible for issuing and managing encryption keys. When a key pair is requested from a CA, it generates a public key and a private key simultaneously, using a specified encryption scheme, such as RSA or DSA. The private key in the pair is given only to the key owner. The public key, on the other hand, can be made available to anyone who needs it. The primary role of the CA is to verify that parties involved in an encrypted exchange are who they say they are. There are two types of CAs that you need to be familiar with:

- Internal CA
- External CA

Because your Linux system installed its own internal CA when you installed the operating system, we can use it to mint our own certificates and use them to encrypt both network transmissions and files in the file system.

Then I discussed how you can use OpenSSH to encrypt remote access sessions between Linux systems. Early Linux network services such as `telnet`, `rlogin`, `rcp`, `rsh`, and FTP transmit data as clear text, which exposes usernames, passwords, and other sensitive data to sniffers. OpenSSH, on the other hand, provides a suite of utilities that you can use to encrypt these data transfers:

- sshd
- ssh
- scp
- sftp
- slogin

OpenSSH uses both private/public key encryption along with secret key encryption. First, the SSH client creates a connection with the system where the SSH server is running on IP port 22. The SSH server then sends its public key to the SSH client. The client system receives the public key from the SSH server and checks to see if it already has a copy of that key. By default, if it doesn’t have the server’s public key in either of these files it will ask the user to add it. Once done, the client now trusts the server system and generates a 256-bit secret key. It then uses the server’s public key to encrypt the new secret key and sends it to the server. The server decrypts it using its private key. Once done, both systems can now use symmetric encryption for the session. In SSH version 2, the secret key is not actually transmitted from the client to the server system. A Diffie-Hellman key agreement is used instead to negotiate a secret key to be used for the session without actually sending it over the network.

The process of configuring OpenSSH involves configuring both the SSH server and the SSH client. You configure the `sshd` daemon using the `/etc/ssh/sshd_config` file. The ssh client is configured using the `/etc/ssh/ssh_config` file or the `~/.ssh/ssh_config` file. Before you can connect to an SSH server, you must open up port 22 in the host-based firewall of the system where `sshd` is running.

You can load the `ssh` client on your local computer and connect to the `sshd` daemon on the remote Linux system by entering `ssh –l user_name ip_address`.

Next, we looked at ways you can tunnel network traffic that is unencrypted by default securely through an SSH tunnel. When client software for the tunneled protocol (such as an e-mail client using POP3) establishes a connection with the local SSH client, the traffic is encrypted using SSH and tunneled through to the SSH server. On the SSH server end, the traffic is decrypted and then forwarded to the appropriate target service (such as a POP3 e-mail daemon). The information is encrypted before being transmitted, even though the original protocol (such as POP3) doesn’t support encryption.

To configure an SSH tunnel, you have to first edit the `/etc/ssh/sshd_config` file on the system where `sshd` is running and set the `AllowTcpForwarding` parameter to a value of `yes`. Then you create a local `ssh` tunnel from a local high IP port to the port on the remote server that the desired service is listening on (such as port 110 for a POP3 server). This is done using the following command:

```
ssh –f –N –L high_port:remote_host_address:port user_name@remote_host_address
```
