Shared client libraries.

+   - `MySQL-bench-version-platform-cpu.rpm`
+   Benchmarks and tests. These require Perl DBI support. (See Section A.4.4, “Installing Perl DBI Support on Unix.”)

+   - `MySQL-version.src.rpm`
+   The source for the server, clients, benchmarks, and tests.

You don’t need to be in any particular directory when you install an RPM package, because RPMs include information indicating where their contents should be placed. For any RPM package `rpm_file`, you can find out where its contents will be installed with the following command:

```
% rpm -qpl  rpm_file
```

To install an RPM package, use this command (you’ll need to do this as *root*):

```
# rpm -i  rpm_file
```

Various parts of MySQL are divided into different RPM packages, so you may need to install more than one RPM. For a typical installation, you should install both the server and client RPMs. If you install only the server RPM, you won’t be able to do much with it, because it doesn’t include the client programs.

For server support, use this command:

```
# rpm -i MySQL-version-platform-cpu.rpm
```

To install the client programs, use this command:

```
# rpm -i MySQL-client-version-platform-cpu.rpm
```

If you plan to write your own programs using the client programming support, make sure to install the development RPM package:

```
# rpm -i MySQL-devel-version-platform-cpu.rpm
```

If you want to install MySQL from the source RPM package, the following command should be sufficient:

```
# rpmbuild --recompile --clean MySQL-version.src.rpm
```

Now proceed to Section A.4.3, “Post-Installation Steps.”

# A.4.2.3  Installing a Source Distribution

MySQL source distributions have names such as *mysql-version.tar.gz*, where *version* is the MySQL version number. (Unlike binary distributions, source distributions apply to all systems, so there are no *platform* or *cpu* values in the filename.) Pick the directory under which you want to unpack the distribution and move into it. Obtain the distribution file and unpack it using one of the following commands (use the second command if your version of *tar* doesn’t understand the *z* option):