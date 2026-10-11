premier and easiest to use being Debian's Automated Package Tool (APT) repositories.

On the commercial side of Linux distributions, several vendors offer online updates, most of them for a fee. Red Hat offers the Red Hat Network (RHN), which is an excellent tool and worth paying for if you run Red Hat for a living. SuSE/Novell offers an online update via YAST, and Mandrake has its Mandrake Online offering.

If you do choose to update packages by hand, never install a security-related package without verifying the package is what it appears to be.

# ## Validation Methods

The two main methods of verifying package authenticity are the MD5 checksum that's calculated and included in the package and a GNU Privacy Guard (GPG or GnuPG) signature for the file.

The MD5 checksum included in a package can be checked easily by running the command shown here:

```
```
rpm -K gentoo-0.11.39-1-fr.i386.rpm
```
```

The command produces output similar to the following:

```
```
gentoo-0.11.39-1-fr.i386.rpm: md5 (GPG) NOT OK (MISSING KEYS: GPG#E42D547B)
```
```

The MD5 checksum in the package is there to be compared against when you run the validation on the package, so it's never supposed to be missing. Someone could have altered the checksum after modifying the package, though, so you should check whether the vendor or package maintainer has a separate .md5 file for the package.

The other mechanism for checking package authenticity is the GPG, which is essentially a method of signing the package with the developer or maintainer's GnuPG key, thus guaranteeing authenticity.

In the previous example you see that the GPG signature is not ok; then a listing of the missing key (GPG#E42D547B) is shown. The gentoo file manager is available from http://www.obsession.se/gentoo/ or from the gentoo.sourceforge.net project page, but the missing GPG key is not easy to find.

If I have a hard time finding the developer's key, I usually get GPG to do the heavy lifting for me and refer to the MIT PGP site (http://pgp.mit.edu) for help.