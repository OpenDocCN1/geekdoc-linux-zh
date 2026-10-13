The corporate_policies.pdf file is then installed, with 0644 permissions, in the directory just created.

```
install -d -m 0755 $RPM_BUILD_ROOT/opt/CorPor-1.0
install -m 0644 corporate_policies.pdf $RPM_BUILD_ROOT/opt/CorPor-1.0/corporate_
policies.pdf
```

After the source code is compiled, it is cleaned with the following directive:

```
%clean
rm -rf $RPM_BUILD_ROOT
```

The locations of the files and directories can be confirmed:

```
%files
$dir /opt/CorPor-1.0
%defattr(-,root,root,-)
/opt/CorPor-1.0/corporate_policies.pdf
```

If desired, you can set up different ownership. For example, if user and group michael were substituted for root in the %defattr(-,root,root,-) directive, the corporate_policies.pdf file that follows would be owned by the user and group michael.

Once the changes are made, you can proceed with the building of an RPM.

# Build Your Own RPM

With the packages installed so far in this chapter, the rpmbuild -ba command can be run by a regular user to create binary and source RPM packages. For the corpor.spec file just described, user michael, from his home directory, could build the RPM from the directives specified in that file with the following command:

```
$ rpmbuild -ba rpmbuild/SPECS/corpor.spec
```

If successful, the last message should indicate success, as follows:

```
+ exit 0
```

If there's a problem, the last message might provide a clue. For example, the following message is straightforward, associated with a typographical error in a file. It also shows the location of the $RPM_BUILD_ROOT variable in the .spec file.

```
RPM build errors:
File not found: /home/michael/rpmbuild/BUILDROOT/CorPor-1.0-1.e16.x86_64/
opt/CorPor-1.0/corporate_policies.pdf
```