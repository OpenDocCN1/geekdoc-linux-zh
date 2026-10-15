
# LAB 101

## Securing Data with Encryption: GPG

### Lab Objective

Learn how to operate `gpg` for data encryption and verification.

### Lab Purpose

In this lab, you will learn about `gpg`, a tool used to encrypt, decrypt, sign, and verify data of files, e-mails, and package updates, among other things.

### Lab Tool

`ubuntu` 18.04 (or another distro of your choice)

### Lab Topology

A single `linux` machine, or virtual machine

### Lab Walkthrough

#### Task 1

Open the `terminal` and run: `gpg --generate-key`

You will be prompted for a name and e-mail address, then `gpg` will do the rest. Afterwards, run `gpg --generate-key` again to create a second key for a different fictitious person.

List the keys you created with `gpg -k`

Finally, take a peek at `~/.gnupg`. In this directory, you should see a trust database (`trustdb.gpg`) and public keyring (`pubring.kbx`), as well as an `openpgp-revocs.d` directory for revocation certificates, and `private-keys-v1.d` directory containing your private key files.

#### Task 2

Now let’s try sending a secret message between your two imaginary `gpg` users:

- `echo "Hello World" > secret`
- `gpg -se -r [email1|2] secret`
- `file secret.gpg`
- `gpg -d < secret.gpg`
