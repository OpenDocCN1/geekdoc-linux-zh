# ### Using GnuPG

GnuPG encryption is currently supported by most mail clients, including Kmail, Thunderbird, and Evolution. You can also use the GNU Privacy Assistant (GPA), a GUI front end, to manage GPG tasks, or you can use the **gpg** command to manually encode and decode messages, including digital signatures, if you wish. As you perform GPG tasks, you will need to reference the keys you have using their key names. Bear in mind that you only need a unique identifying substring to select the key you want. GPG performs a pattern search on the string you specify as the key name in any given command. If the string matches more than one key, all those matching values will be selected. In the following example, the “Sendmail” string selects matches on the identities of two keys.

```
```
# gpg  --list-keys "Sendmail"
  pub  1024R/CC374F2D 2000-12-14
          Sendmail Signing Key/2001 <sendmail@Sendmail.ORG>
  pub  1024R/E35C5635 1999-12-13
          Sendmail Signing Key/2000 <sendmail@Sendmail.ORG>
```
```

# ### Encrypting Messages

The **gpg** command provides several options for managing secure messages. The **e** option encrypts messages, the **a** option generates an armored text version, and the **s** option adds a digital signature. You will need to specify the recipient’s public key, which you should already have imported into your **pubring** file. It is this key that is used to encrypt the message. The recipient will then be able to decode the message with their private key. Use the **--recipient** or **-r** option to specify the name of the recipient key. You can use any unique substring in the user’s public key name. The e-mail address usually suffices. You use the **d** option to decode received messages. In the following example, the user encrypts (**e**) and signs (**s**) a file generated in armored text format (**a**). The **-r** option indicates the recipient for the message (whose public key is used to encrypt the message).

```
```
gpg e -s -a -o myfile.asc -r george@rabbit.mytrek.com myfile
# mail george@rabbit.mytrek.com < myfile.asc
```
```

You can leave out the ASCII armor option if you want to send or transfer the file as a binary attachment. Without the **-armor** or **-a** option, **gpg** generates an encoded binary file, not an encoded text file. A binary file can be transmitted through e-mail only as an attachment. As noted previously, ASCII armored versions usually have an extension of **.asc**, whereas binary versions use **.gpg**.

> ***NOTE*** *You can use* ***gpgsplit*** *to split a GPG message into its components in order to examine them separately.*

# ### Decrypting Messages

When the other user receives the file, they can save it to a file named something like **myfile.asc** and then decode the file with the **-d** option. The **-o** option will specify a file to save the decoded version in. GPG will automatically determine if it is a binary file or an ASCII armored version.

```
```
gpg -d -o myfile.txt myfile.asc
```
```