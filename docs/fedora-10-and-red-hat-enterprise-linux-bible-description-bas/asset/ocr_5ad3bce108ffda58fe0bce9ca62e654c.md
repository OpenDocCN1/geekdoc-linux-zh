# Part II: Using Fedora and RHEL

the dvgrab RPM (which is part of Fedora) in my local directory and I wanted to check it. I could run the following command:

```
# rpm --checks dvgrab-3.2-1.fc10.rpm
dvrgrab:3.2-1.fc10.i386.rpm (sha) sha md5 gpg OK
```

The preceding output shows that the GPG/DSA key was found and used to check that the package's digital signatures (dsa, sha, and md5) were correct. However, if you got a package for which you didn't have the GPG/DSA key installed, you would need to get and import that key before you could verify the package.

If you trust the Internet where you are getting the RPM you want to install, look for an indication that the site has signed its packages. Download the GPG public key and import it. That will allow you to check the validity of the packages from that site. For example, I decided to use the KDE-red (http://apt.kde-redhat.org) project to replace all MY packages from Fedora. I downloaded the digikam package and tried to verify it as:

```
# rpm --checks digikam-doc-0.9.4-2.fc10.rpm
digikam-doc-0.9.4-2.fc10.rpm:(SHA1) DSA sha md5 (GPG) NOT OK (MISSING KEYS: GPG#ff6382fa)
```

Because the GPG public key was not installed, the contents couldn't be verified as correct. I went to the KDE-red project site and downloaded the GPG public key to the current directory. I imported the key as follows:

```
# rpm --import gpg-pubkey-ff6382fa-3e1ab2ca
```

With the GPG public key imported, the second check of the RPM showed it was clean:

```
# rpm --checks digikam-doc-0.9.4-2.fc10.rpm
digikam-doc-0.9.4-2.fc10.rpm:(sha) dsa sha md5 gpg OK
```

Most of the public keys you need for the basic repositories used with Fedora in the fedora-release package. GPG public keys from other repositories are stored with those in the /etc/pki/rpm-gpg directory.

Remember, however, it is best to get packages automatically from known repositories with yum (or related tools). Besides checking the signatures of packages, yum will also make sure all dependencies are cleared up.

# Installing with rpm

To install an RPM file that is not yet installed on your system with the rpm command, most people generally use the same options if they were upgrading the (-U option). Here's an example of a line you could use to install a new RPM package:

```
# rpm -U [options] package
```