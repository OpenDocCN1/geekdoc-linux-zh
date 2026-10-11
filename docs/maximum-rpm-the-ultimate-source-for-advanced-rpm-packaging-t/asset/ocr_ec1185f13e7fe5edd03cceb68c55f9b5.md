Because of this, it’s important that the spec file and the makefile be written in such a way that no assumptions about the build root are made. The main issue is that the build root must not be hard-coded anywhere. Always use the `RPM_BUILD_ROOT` environment variable!

Another issue to keep in mind is cleaning up after the build. Once software builds and is packaged successfully, it’s probably no longer necessary to leave the build tree in place. Therefore, it’s a good idea to include the necessary commands in the spec file’s `%clean` section. Here’s an example:

```
%clean
rm -rf $RPM_BUILD_ROOT
```

Since RPM executes the `%clean` section after the binary package has been created, it’s the perfect place to delete the build root tree. In this example, that’s exactly what we’re doing. We’re also doing the right thing by using `RPM_BUILD_ROOT` instead of a hard-coded path.

The last issue to keep in mind relates to the `%clean` section we just created. At the start of the chapter, we mentioned that it’s not a good idea to define a build root of `/`. The `%clean` section is why: If the build root were set to `/`, the `%clean` section would blow away your root filesystem! Keep in mind that this can bite you, even if the package’s spec file doesn’t specify `/` as a build root. It’s possible to use the `--buildroot` option to specify a dangerous build root, too:

```
# rpm -ba --buildroot / cdpairs-1.0.spec
```

But for all the possible hazards using build roots can pose for the careless, it’s the only way to prevent a build from disrupting the operation of certain packages on the build system. And for the person wanting to build packages without root access, it’s the first of three steps necessary to accomplish the task. The next step is to direct RPM to build the software in a directory other than RPM’s default one.

# ## 16.2. Having RPM Use a Different Build Area

While RPM’s build root requires a certain amount of spec file and makefile tweaking in order to get it working properly, directing RPM to perform the build in a different directory is a snap. The hardest part is to create the directories RPM will use during the build process.

# ### 16.2.1. Setting Up a Build Area

RPM’s build area consists of five directories in the top level:

+   - The `BUILD` directory is where the software is unpacked and built.
+   - The `RPMS` directory is where the newly created binary package files are written.
+   - The `SOURCES` directory contains the original sources, patches, and icon files.
+   - The `SPECS` directory contains the spec files for each package to be built.
+   - The `SRPMS` directory is where the newly created source package files are written.