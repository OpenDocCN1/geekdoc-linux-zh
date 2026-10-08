per word and provides very poor phrases.) You can change the passphrase later with
the -p option.

There is no way to recover a lost passphrase. If the passphrase is lost or forgotten, you
have to generate a new key and copy the corresponding public key to other machines.

For RSA, there is also a comment field in the key file that is only for convenience to
t user to help identify the key. The comment can tell what the key is for or whatever
is useful. The comment is initialized to user@host when the key is created but can be
changed with the -c option.

After a key is generated, instructions below detail where to place the keys to activate
them.

# Options

+   -b bits Specify the number of bits in the key to create. The minimum number
is 512 bits. Generally, 1024 bits are considered sufficient. Key sizes
above that no longer improve security but make things slower.
default is 1024 bits.

+   -c Change the comment in the private and public key files. The command
prompts for the file containing the private keys, for the passphrase if
key has one, and for the new comment.

+   -C comment Specify the new comment.

+   -f input_keyfile Specify the file name of the key file.

+   -1 Show the fingerprint of the specified private or public key.

+   -N new_passphrase Provide the new passphrase.

+   -p Change the passphrase of a private key file instead of creating a new
private key. The command prompts for the file containing the private key
for the old passphrase, and twice for the new passphrase.

+   -P passphrase Provide the (old) passphrase.

+   -q Silence ssh-keygen. Used by /etc/rc when creating a new key.

+   -R If support is functional, immediately exit with code 0. If RSA
support is not functional, exit with code 1. This option will be removed
when the RSA patent expires.

+   -x Read a private OpenSSH DSA format file, and print an
SSH2-compatible public key to standard output.

+   -X Read an unencrypted SSH2-compatible private (or public) key file, and
print an OpenSSH compatible private (or public) key to standard
output.

+   -y Read a private OpenSSH DSA format file, and print an OpenSSH DSA
public key to standard output.