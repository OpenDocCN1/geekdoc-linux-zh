
Pick your RSA key size:

- 512 bits – Low commercial grade, fast but less secure
- 768 bits – High commercial grade, medium speed, good security
- 1024 bits – “Military” grade, slow, highest security

Choose 1, 2, or 3, or enter desired number of bits: 3
Generating an RSA key with a 1024-bit modulus.

You need a user ID for your public key. The desired form for this user ID is your name, followed by your E-mail address enclosed in <angle brackets>, if you have an E-mail address.

For example: John O. Smith <12345.6789@compsers.com>

Enter a user ID for your public key:

### Example Key for RPM Book

You need a pass phrase to protect your RSA secret key. Your pass phrase can be any sentence or phrase and may have many words, spaces, punctuation, or any other printable characters.

Enter pass phrase: `<passphrase>` (Not echoed)

Enter same pass phrase again: `<passphrase>` (Still not echoed)

Note that key generation is a lengthy process.

We need to generate 952 random bits. This is done by measuring the time intervals between your keystrokes. Please enter some random text on your keyboard until you hear the beep:

(Many random characters were entered)

0* - Enough, thank you.

..*..*...***...****..*..****..*....*..***..*..****..*....

Pass phrase is good. Just a moment....
Key signature certificate added.
Key generation completed.

Let’s review each of the times PGP required information. The first thing PGP needed to know was the key size we wanted. Depending on your level of paranoia, simply choose an appropriate key size. In our example, we chose the “They’re out to get me” key size of 1,024 bits.

Next, we needed to choose a user ID for the key. The user ID should be descriptive and should also include sufficient information for someone to contact you. We entered Example Key for RPM Book, which goes against this suggestion but is sufficient for the purposes of our example.

After entering a user ID, we needed to add a passphrase. The passphrase is used to protect your secret key, so it should be something difficult for someone else to guess. It should also be memorable for you, because if you forget your passphrase, you won’t be able to use your secret key! I entered a couple words and numbers, put together in such a way that no one could ever guess I typed rpm2kool4words....Oops!

The passphrase is entered twice to ensure that no typing mistakes were made. PGP also performs some cursory checks on the passphrase, ensuring that the phrase is at least somewhat secure.

Finally comes the strangest part of the key-generation process: creating random bits. This is done by measuring the time between keystrokes. The secret here is to not hold down a key so that it auto-repeats and to not wait several seconds between keystrokes. Simply start typing anything (even nonsense text) until PGP tells you’ve typed enough.

After generating enough random bits, PGP takes a minute or so to create the key. Assuming that everything completed successfully, you’ll see an ending message similar to the one shown in this example. You’ll also find, in a subdirectory of your login directory called `.ppp`, the following files:

```
# ls -al - /.ppp
total 6
drwxr-xr-x    2 root    root    1024 Oct 30 19:44 .
drwxr-xr-x    5 root    root    1024 Oct 30 19:44 ..
-rw------     1 root    root      176 Oct 30 19:44 pubring.bak
-rw-------     1 root    root      331 Oct 30 19:44 pubring.pgp
-rw-------     1 root    root      408 Oct 30 19:44 random.seed.bin
-rw-------     1 root    root      509 Oct 30 19:44 secring.pgp
#
```

Those of you interested in learning exactly what each file is can consult any of the fine books on PGP. For the purposes of signing packages, all you need to know is where these files are located.

That’s it! Now it’s time to configure RPM to use your newly generated key.

## 17.2.2. Preparing RPM

RPM’s configuration process is quite straightforward. It simply consists of adding a few rpmsrc entries in a file of your choice. For more information on rpmsrc files in general, see Appendix B, “The rpmsrc File.”

The entries that need to be added to an rpmsrc file are

- signature
- pkg_name
- ppg_path

Let’s check out the entries:

- **signature**—The signature entry is used to select the type of signature that RPM is to use. At the time this book is being written, the only legal value is ppg. So you would enter:

```
signature: ppg
```

- **ppg_name**—The ppg_name entry gives RPM the user ID of the key it is to sign packages with. In our key-generation example, the user ID of the key we created was Example Key for RPM Book, so this is what our entry should look like:

```
ppg_name: Example Key for RPM Book
```

- **ppg_path**—The ppg_path entry is used to define the path to the directory where the keys are kept. This entry is not needed if the environment variable PPPATH has been defined. In our example, we didn't move them from PGP's default location, which is in the subdirectory .ppg, off the user's login directory. Because we generated the key as root, our path is /root/.ppg. Therefore, our entry would look like this:

```
ppg_path: /root/.ppg
```

And that's it. Now it's time to sign some packages.

## 17.3. Signing Packages

There are three different ways to sign a package:

- Sign the package at build time.
- Replace the signature on an already-existing package.
- Add a signature to an already-existing package.

Let's take a look at each one, starting with build time signing.

### 17.3.1. --sign: Sign a Package at Build Time

The --sign option is used to sign a package as it is being built. When this option is added to an RPM build command, RPM will ask for your PGP passphrase. If the passphrase is correct, the build will proceed. If not, the build stops immediately.

Here's an example of --sign in action:

```
# rpm -ba --sign blather-7.9.spec
Enter pass phrase: <passphrase> (Not echoed)

Pass phrase is good.
* Package: blather
...
Binary Packaging: blather-7.9-1
Finding dependencies...
...
Generating signature: 1002
Wrote: /usr/src/redhat/RPMS/i386/blather-7.9-1.i386.rpm
...
Source Packaging: blather-7.9-1
...
Generating signature: 1002
Wrote: /usr/src/redhat/SRPMS/blather-7.9-1.src.rpm
#
```

Once the passphrase is entered, there's very little that is different from a normal build. The only obvious difference is the **generating signature** message in both the binary and source packaging sections. The number following the message indicates that the signature added was created using PGP. (The list of possible signature types can be found in the RPM sources, specifically *signature.h*, in RPM's *lib* subdirectory.)

Notice that since RPM only signs the source and binary package files, only the `--bb` and `-ba` options make any sense when used with `--sign`. This is due to the fact that only the `--bb` and `-ba` issues create package files.

If we issue a quick signature check using RPM's `--checksig` option, we can see that there is, in fact, a PGP signature present:

```
# rpm --checksig blather-7.9.1.i386.rpm
blather-7.9.1.i386.rpm: size vpp m5 OK
#
```

It's clear that, in addition to the usual size and MD5 signatures, the package has a PGP signature.

#### 17.3.1.1. Multiple Builds? No Problem!

You might be wondering how the `--sign` option will work if more than one package is to be built. Do you have to enter the passphrase for every single package you build? The answer is no, so long as you build the packages with a single RPM command. Here's an example:

```
# rpm -ba --sign b*.spec
Enter pass phrase: <passphrase> (Not echoed)

Pass phrase is good.

* Package: blather
..
Binary Packaging: blather-7.9.1
..
Generating signature: 1002
Wrote: /usr/src/redhat/RPMS/i386/blather-7.9.1.i386.rpm
..
Source Packaging: blather-7.9.1
..
Generating signature: 1002
Wrote: /usr/src/redhat/SRPMS/blather-7.9.1.src.rpm
..
* Package: bother
..
Binary Packaging: bother-3.5.1
..
Generating signature: 1002
Wrote: /usr/src/redhat/RPMS/i386/bother-3.5.1.i386.rpm
..
Source Packaging: bother-3.5.1
..
Generating signature: 1002
Wrote: /usr/src/redhat/SRPMS/bother-3.5.1.src.rpm
#
```
