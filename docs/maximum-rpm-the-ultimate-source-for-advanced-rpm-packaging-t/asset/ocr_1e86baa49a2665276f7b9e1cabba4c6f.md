# ### E.3. Scripts

Scripts are used by RPM to perform processing at various times.

# #### E.3.1. Build Time Scripts

Every build time script has the following environment variables defined:

+   - RPM_SOURCE_DIR
+   - RPM_BUILD_DIR
+   - RPM_DOC_DIR
+   - RPM_OPT_FLAGS
+   - RPM_ARCH
+   - RPM_OS
+   - RPM_ROOT_DIR
+   - RPM_BUILD_ROOT
+   - RPM_PACKAGE_NAME
+   - RPM_PACKAGE_VERSION
+   - RPM_PACKAGE_RELEASE

For more information on these environment variables and build time scripts, see section 13.3.1 in Chapter 13.

# ##### E.3.1.1. The %prep Script

The %prep script is the first script RPM executes during a build:

```
%prep
```

As the name implies, it is normally used to prepare the sources for building. The commands in the script can be any valid sh commands.

# ##### E.3.1.2. The %build Script

The %build script is the second script RPM executes during a build:

```
%build
```

As the name implies, it is normally used to build the software. The commands in the script can be any valid sh commands.