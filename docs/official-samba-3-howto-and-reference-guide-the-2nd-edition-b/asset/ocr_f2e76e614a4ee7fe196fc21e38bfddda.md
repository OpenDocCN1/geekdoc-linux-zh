transfer only the data that is missing plus a small overhead. See the rsync home page⁵ for more info on rsync.

The disadvantage of the unpacked trees is that they do not support automatic merging of local changes as Subversion does. **rsync access** is most convenient for an initial install.

# ## 40.3  Verifying Samba’s PGP Signature

It is strongly recommended that you verify the PGP signature for any source file before installing it. Even if you’re not downloading from a mirror site, verifying PGP signatures should be a standard reflex. Many people today use the **GNU GPG** tool set in place of PGP. **GPG** can substitute for PGP.

With that said, go ahead and download the following files:

```
$ wget http://us1.samba.org/samba/ftp/samba-3.0.20.tar.asc
$ wget http://us1.samba.org/samba/ftp/samba-pubkey.asc
```

The first file is the PGP signature for the Samba source file; the other is the Samba public PGP key itself. Import the public PGP key with:

```
$ gpg --import samba-pubkey.asc
```

and verify the Samba source code integrity with:

```
$ gzip -d samba-3.0.20.tar.gz
$ gpg --verify samba-3.0.20.tar.asc
```

If you receive a message like, “**Good signature from Samba Distribution Verification Key...**” then all is well. The warnings about trust relationships can be ignored. An example of what you would not want to see would be:

```
gpg: BAD signature from Samba Distribution Verification Key
```

# ## 40.4  Building the Binaries

After the source tarball has been unpacked, the next step involves configuration to match Samba to your operating system platform. If your source directory does not contain the **configure-script**, it is necessary to build it before you can continue. Building of the configure