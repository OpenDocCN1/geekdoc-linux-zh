By now, the opening **if** statement is an old friend. As you might have expected, we are verifying whether the client package is installed by looking for a file from that package. If the client package isn't there, the entry is removed from /etc/services. And that is that.

Obviously, these scripts must be carefully tested. In the case of amanda, because the two packages have some measure of interdependency, it's necessary to try different sequences of installing and erasing the two packages to make sure the /etc/services logic works properly in all cases.

After a bit of testing, our install and uninstall scripts pass with flying colors. From a technical standpoint, the client and server subpackages are ready to go.

# 20.4.3.3. Bits and Pieces

However, just because a package has been properly built and installs and can be erased without problems doesn't mean that the package-builder's job is done. It's necessary to look at each newly built package from the user's perspective. Does the package contain everything users needs in order to deploy it effectively? Or will users need to fiddle with it, guessing as they go?

In the case of our amanda packages, it was obvious that some additional documentation was required so that the user would know what needed to be done to finalize the installation. Simply directing the user to the standard amanda documentation wasn't the right solution, either. Many of the steps outlined in the INSTALL document had already been done by the postinstall scripts. No, an interim document was required. Two, actually: one for the client, and one for the server.

So two files were created, one to be added to each subpackage. The question was, how to do it? Essentially, there were two options:

+   • Put the files in the amanda directory tree that had been used to perform the initial builds and generate a new patch file
+   • Create a tar file containing the two files, and modify the spec file to unpack the documentation into the amanda directory tree
+   • Drop the files directly into the amanda directory tree without using tar

Since the second approach was more interesting, that's the approach we chose. It required an additional source tag in the spec file:

```
Source1: amanda-rpm-instructions.tar.gz
```

Also required was an additional %setup macro in the %prep script:

```
%setup -T -D -a 1
```

While the %setup macro might look intimidating, it wasn't that hard to construct. Here's what each option means:

-T —Do not perform the default archive unpacking.