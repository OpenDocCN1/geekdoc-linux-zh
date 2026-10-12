The message is encrypted using my public key (without any signature, but you can add the signature with an `-s` command).

When I receive the `message.gpg` file, I have to decrypt it using my private key. Here’s the command I use:

```
`gpg -o message --decrypt message.gpg`
```

GPG then prompts me for the passphrase to unlock my private key and then decrypts the message and saves the output in the file named `message`.

If you simply want to encrypt a file and no one else has to decrypt the file, you can use GPG to perform what is called *symmetric encryption*. In this case, you provide a passphrase to encrypt the file with the following GPG command:

```
`gpg -o secret.gpg -c somefile`
```

GPG prompts you for the passphrase and asks you to repeat the passphrase (to make sure that you didn’t mistype anything). Then GPG encrypts the file using a key generated from the passphrase.

To decrypt a file encrypted with a symmetric key, type

```
`gpg -o myfile --decrypt secret.gpg`
```

GPG prompts you for the passphrase. If you enter the correct passphrase, GPG decrypts the file and saves the output (in this example) in the file named `myfile`.

# ## *Monitoring System Security*

Even if you secure your system, you have to monitor the log files periodically for signs of intrusion. You may want to install the Tripwire software to monitor the integrity of critical system files and directories. Fedora Core does not come with the Tripwire package. To use Tripwire, you have to download it from `www.tripwire.org/downloads/index.php`. You have to download the source tarball (a compressed archive of source files) and then build Tripwire. (Book VI, Chapter 4 provides more information on how to build software packages from source files.) After you build and install Tripwire, you can configure it to monitor any changes to specified system files and directories on your system.

Periodically examine the log files. Many Fedora Core applications, including some servers, write log information using the logging capabilities of `syslogd`.