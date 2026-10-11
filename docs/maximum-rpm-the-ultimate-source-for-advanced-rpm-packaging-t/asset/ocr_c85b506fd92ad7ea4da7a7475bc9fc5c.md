# C.4.1. Options for Verify Mode

The following options can be used on any verify command:

+   - -nodeps—Do not verify package dependencies.
+   - -nofiles—Do not verify file attributes.
+   - -noscripts—Do not execute the package’s verification script.

# C.5. Install Mode

RPM’s installation mode is used to install packages.

Format:

```
rpm --install <package file>
```

```
or
```

```
rpm -i <package file>
```

# C.5.1. Options for Install Mode

The following options can be used on any install command:

+   - -h, --hash—Print hash marks as package installs (good with -v).
+   - --prefix <dir>—Relocate the package to <dir>, if relocatable.
+   - --excludedocs—Do not install documentation.
+   - --force—Shorthand for --replacepkgs and --replacefiles.
+   - --ignorescripts—Do not verify package architecture.
+   - --ignorescripts—Do not verify package operating system.
+   - --includedocs—Install documentation.
+   - --nodeps—Do not check package dependencies.
+   - --noscripts—Do not execute any installation scripts.
+   - --percent—Print percentages as package installs.
+   - --replacefiles—Install even if the package replaces installed files.
+   - --replacepkgs—Reinstall if the package is already present.
+   - --test—Do not install, but tell whether it would work.